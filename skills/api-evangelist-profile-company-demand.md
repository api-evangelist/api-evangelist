---
name: profile-a-companys-api-demand
description: Read the demand side for one company — its 40-dimension technology readiness, the stack it has adopted, and where it is thin — from the API Evangelist Insights corpus.
api: openapi/apievangelist-v1-openapi.yml
base_url: https://api.apievangelist.com/v1
auth: keyless for browse and ranking; x-api-key for the gaps analysis
operations: [getInsightsSummary, listInsightCompanies, listInsightIndustries, listInsightDimensions, listInsightAdoption, getCompanyInsight, getCompanyGaps]
generated: '2026-08-10'
method: generated
source: openapi/apievangelist-v1-openapi.yml
---

# Profile a company's API demand

Use this before a vendor conversation, an account plan, or a sector write-up — it is the
demand-side view (what companies are hiring for and investing in), not a supply-side catalog of
what they publish.

## Before you start

- Base URL `https://api.apievangelist.com/v1`, keyless for most of this flow.
- Insights covers profiled companies (Fortune 1000 and API providers) across 40 tracked
  investment dimensions.
- These seven operations are live in the contract but are **absent from the published
  `x-apis-io.operations` experience map**, so tooling built off that map will not know about
  `getInsightsSummary` or `listInsightIndustries` at all. Call them directly.

## Steps

1. **Orient.** `getInsightsSummary` — `GET /insights` — what the corpus covers and how big it is.
2. **Find the company.** `listInsightCompanies` — `GET /insights/companies?q=<name>`. Results are
   ranked; confirm you have the right entity before going deeper, and check the slug.
3. **Read the profile.** `getCompanyInsight` — `GET /insights/company/{slug}` — the
   40-dimension readiness read plus the adopted stack.
4. **Find the thin spots.** `getCompanyGaps` — `GET /insights/company/{slug}/gaps` — the weakest
   dimensions. **Pro** — returns `403 upgrade_required` without a key.
5. **Put it in context.** `listInsightDimensions` — `GET /insights/dimensions` — cross-section
   ranking of the 40 dimensions, so "weak on governance" can be stated relative to the field
   rather than in the abstract.
6. **Check the sector.** `listInsightIndustries` — `GET /insights/industries` — for the peer set.
7. **Check what the market actually adopts.** `listInsightAdoption` —
   `GET /insights/adoption` — services, tools or standards ranked by adopting-company count.

## Error handling

- `404 not_found` — the company slug is wrong. Always resolve via `listInsightCompanies` first;
  do not construct a slug from a company name.
- `403 {"error":"upgrade_required","tier":"pro"}` — `getCompanyGaps` is Pro. Degrade to
  `getCompanyInsight` plus `listInsightDimensions` and say the gaps read was unavailable rather
  than inferring it.
- No `429` or `5xx` declared in the contract.

## Care with this data

- Company corpora are attributed by source; a profile is a read of public demand signal, not a
  statement from the company. Attribute it that way in anything you write.
- All operations are `GET` and safe to retry.

See `conventions/api-evangelist-conventions.yml` and
`mcp/api-evangelist-tool-crosswalk.yml` (Insights tools are bound there by name, not by the
first-party map).
