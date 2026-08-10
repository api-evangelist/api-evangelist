---
name: make-an-api-agent-ready
description: Turn an existing OpenAPI into a governed agent surface — forge MCP tools and Agent Skills from it, gate which operations and fields agents may see, emit an llms.txt and AGENTS.md, and map the API to MCP to Agent Skill journey.
api: openapi/apievangelist-governance-openapi.json
base_url: https://api.apievangelist.com/v1
auth: x-api-key required — every operation in this flow is Pro
operations: [classify, contextGate, toolsmith, agentDescriptor, experience, agentExport, reusability, onboarding]
generated: '2026-08-10'
method: generated
source: openapi/apievangelist-governance-openapi.json
---

# Make an API agent-ready

Use this when a team wants to expose an existing REST API to AI agents without handing agents the
whole surface.

## Before you start

- Base URL `https://api.apievangelist.com/v1`; all `POST`; the spec goes in the `document` body
  field.
- **This whole flow is Pro.** Expect `402 {"error":"payment_required"}` without `x-api-key`.
  Get a key at `GET /v1/auth/login`, plans at https://developer.apievangelist.com/plans/.
- Do the steps in this order — gating before forging. Forging tools from an ungated spec is how
  an agent ends up with a `DELETE` tool nobody meant to publish.

## Steps

1. **Find what must never reach an agent.** `classify` —
   `POST /governance/classify` inventories the PII, secret and sensitive fields across
   parameters, request bodies and responses. This is the input to step 2, not an afterthought.
2. **Gate the surface.** `contextGate` — `POST /governance/context-gate`. Choose which operations
   and which fields the API exposes to agents and get back a governed context contract. Anything
   `classify` flagged should be excluded here or justified.
3. **Forge the tools.** `toolsmith` — `POST /governance/toolsmith` takes the (gated) OpenAPI and
   returns an MCP server design, per-operation tools with real input schemas inherited from the
   spec's `parameters` and `requestBody`, and Agent Skills.
4. **Publish the consumption contract.** `agentDescriptor` —
   `POST /discovery/agent-descriptor` emits the API's `llms.txt` and an `AGENTS.md`: base URL,
   auth, the operations an agent may call, and the rules for calling them.
5. **Turn governance into agent guidance.** `agentExport` —
   `POST /governance/agent-export` converts a ruleset into an `AGENTS.md` block and system prompt,
   so the agent is told the same rules CI enforces.
6. **Map the journey.** `experience` — `POST /discovery/experience` maps each REST operation to
   its MCP tool and Agent Skill. Compare the result against the crosswalk you already keep — for
   this network that is `mcp/api-evangelist-tool-crosswalk.yml`.
7. **Check you are not duplicating.** `reusability` — `POST /discovery/reusability` scores a
   *set* of APIs for duplication before you mint a second agent surface over the same data.
8. **Validate the onboarding descriptor.** `onboarding` — `POST /discovery/onboarding` checks an
   API Onboarding Descriptor (AID) against the api-commons schema.

## Error handling

- `402 payment_required` — Pro. The response carries `upgrade` and `signup` URLs; do not retry
  the same request without a key.
- `400 bad_request "Missing required field: document."` — the spec was not sent in `document`.
- `422` — the document did not parse.
- No `429` or `5xx` declared. Back off.

## Conventions that apply

- Stateless compute; retries are safe for every operation in this flow (none of them mints a
  durable artifact — that is `certify`, which is not part of this skill).
- Error envelope is `{error, message}` on this API.
- Bulk input is Pro; the free tier accepts one document per call.

See `mcp/api-evangelist-tool-crosswalk.yml` and
`agentic-access/api-evangelist-agentic-access.yml` for what this looks like applied to API
Evangelist's own surface.
