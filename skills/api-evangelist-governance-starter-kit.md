---
name: assemble-a-governance-starter-kit
description: Pull a working API governance starter kit out of the API Evangelist network — the guidance, rules, policies, standards and strategies that apply to one capability, plus how to engage.
api: openapi/apievangelist-v1-openapi.yml
base_url: https://api.apievangelist.com/v1
auth: none required (keyless free tier); x-api-key to inline full bodies
operations: [listGuidance, getGuidanceItem, getGuidanceRelated, listRules, getRulesItem, listPolicies, getPoliciesItem, listStandards, getStandardsItem, listStrategies, getStrategiesItem, listServices, getService]
generated: '2026-08-10'
method: generated
source: openapi/apievangelist-v1-openapi.yml
---

# Assemble a governance starter kit

Use this when a team needs a defensible starting set of governance material for one capability
(pagination, error handling, deprecation, security, agent exposure…).

## Before you start

- Base URL `https://api.apievangelist.com/v1`, keyless.
- Nine building-block collections share one shape: `guidance`, `rules`, `policies`, `standards`,
  `strategies`, `schema`, `properties`, `experiences`, `lifecycle`. Every one supports
  `q`, `tags`, `match=any|all`, `fields`, `sort`, `page`, `limit`.
- Keep `limit` ≤ 100 and read `meta.total` before deciding to paginate.

## Steps

1. **Guidance first — the "why".** `listGuidance` — `GET /guidance?q=<capability>&limit=10`.
   Then `getGuidanceItem` (`GET /guidance/{slug}`) on the two or three that fit, with
   `include=content` for the full body.
2. **Rules — the enforceable "what".** `listRules` — `GET /rules?tags=<capability>&match=all`.
   These are the Spectral-shaped, machine-enforceable rules; `getRulesItem`
   (`GET /rules/{slug}`) gives you one in full. This is the set you feed into
   `POST /governance/validate` (see the `lint-and-score-an-openapi` skill).
3. **Policies — the business reason.** `listPolicies` / `getPoliciesItem`. Policies are what you
   cite when someone asks who decided this.
4. **Standards — the interoperability anchor.** `listStandards` / `getStandardsItem`. Prefer an
   existing standard over an invented convention, and record which one you picked.
5. **Strategies — the sequencing.** `listStrategies` / `getStrategiesItem` for how to roll the
   above out rather than drop it on a team.
6. **Widen without re-querying.** `getGuidanceRelated` (`GET /guidance/{slug}/related`) surfaces
   the related material across every type from any one guidance document.
7. **Close the loop.** `listServices` / `getService` if the team needs someone to do the work —
   these are the engagements API Evangelist offers, not third-party vendors.

## Error handling

- `404 not_found` — the slug is wrong for that collection. Each collection has its own slug
  namespace; a guidance slug is not a rules slug.
- `403 upgrade_required` — `include=content` is Pro on some collections. Degrade to summaries
  rather than retrying with the same request.
- No `429` or `5xx` is declared in the contract. Treat either as an unspecified transient and
  back off.

## Conventions that apply

- All operations are `GET` and safe to retry; there is no idempotency contract because there is
  nothing to mutate.
- Errors are `{error, detail}` JSON, not RFC 9457.
- `tags` + `match=all` is the sharpest filter available; there is no boolean query syntax.

See `conventions/api-evangelist-conventions.yml`.
