---
name: lint-and-score-an-openapi
description: Run an OpenAPI (or AsyncAPI, Arazzo, JSON Schema) through the API Evangelist governance compute layer — lint it, measure how much of it your rules actually inspect, reconcile waivers, score it, and produce a report.
api: openapi/apievangelist-governance-openapi.json
base_url: https://api.apievangelist.com/v1
auth: keyless for the checking operations; x-api-key required for the Pro ones
operations: [rulesets, rules, validate, coverage, waivers, scorecard, report, classify, diff, deprecation, certify, verify]
generated: '2026-08-10'
method: generated
source: openapi/apievangelist-governance-openapi.json
---

# Lint and score an OpenAPI

Use this to check an API description against curated governance rules and produce something a
team can act on.

## Before you start

- Base URL `https://api.apievangelist.com/v1`. Every operation here is a `POST` with the document
  in the JSON request body, except `rules` and `rulesets` which are `GET`.
- **The required body field is `document`.** Omitting it returns
  `400 {"error":"bad_request","message":"Missing required field: document."}`.
- Free tier: keyless, 5 req/s, 1,000 req/day, **one document per call**. Bulk input is Pro.
- `components.schemas` is empty in this contract — request and response shapes are documented in
  prose only, so read `GET /governance/rulesets` output rather than assuming field names.

## Steps

1. **Pick a ruleset.** `rulesets` — `GET /governance/rulesets` lists the named curated rulesets.
   `rules` — `GET /governance/rules` lists the individual rules behind them. Free.
2. **Lint.** `validate` — `POST /governance/validate` with `{"document": <spec>}` and optionally
   your own ruleset. Free. Returns Spectral-shaped findings.
3. **Check your rules actually look at the API.** `coverage` —
   `POST /governance/coverage`. A clean lint against rules that inspect 8% of the document is not
   a clean API. Run this before you report a pass. Free.
4. **Suppress what has been sanctioned.** `waivers` — `POST /governance/waivers` reconciles a
   waivers file against the lint output and flags waivers that no longer match anything. Free.
5. **Score it.** `scorecard` — `POST /governance/scorecard` returns 0–100 with a letter grade
   across design, governance coverage and documentation. Free.
6. **Report it.** `report` — `POST /governance/report` renders a self-contained HTML governance
   report. **Pro** (`402`).
7. **Optional depth**, all `POST`:
   - `classify` — inventory the PII, secret and sensitive fields the spec exposes.
   - `diff` — compare two versions and classify each change breaking / non-breaking.
   - `deprecation` — list every deprecated operation and whether it actually announces a sunset.
   - `certify` (**Pro**) — issue a tamper-evident certificate; `verify` re-checks it against the
     live API and reports drift.

## Error handling

- `400 {"error":"bad_request","message":"Missing required field: document."}` — send the spec in
  `document`.
- `422` on `validate` — the document is not parseable as OpenAPI/AsyncAPI/Arazzo/JSON Schema. Do
  not retry; fix or re-fetch the document.
- `402 {"error":"payment_required", "upgrade": "...", "signup": "..."}` — a Pro capability.
  Note this API returns **402** where the sibling network API returns **403** for the same
  condition. Fall back to the free operations.
- `401` on `/auth/me` and `/billing/checkout` — sign in at `GET /v1/auth/login` first.
- No `429` and no `5xx` are declared. Back off on either.

## Conventions that apply

- **No idempotency key.** These operations are stateless compute over the body you send, so a
  retry is harmless — with one exception: `certify` mints a durable certificate, and a retried
  request issues a **second** certificate. Do not blind-retry `certify`.
- Error envelope here is `{error, message}` — the network API uses `{error, detail}`. Parse both.
- Three operations (`GET /auth/login`, `GET /auth/me`, `POST /billing/checkout`) carry no
  `operationId` in the contract, so they cannot be referenced by id.

See `errors/api-evangelist-problem-types.yml` and `conventions/api-evangelist-conventions.yml`.
