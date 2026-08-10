---
name: map-the-vendor-landscape
description: Map the commercial and open-source tooling landscape for one API capability using the API Evangelist solutions and tools registries, ranked by how many profiled companies actually adopt each one.
api: openapi/apievangelist-v1-openapi.yml
base_url: https://api.apievangelist.com/v1
auth: none required (keyless free tier)
operations: [listSolutions, getSolution, listTools, getTool, listInsightAdoption, listStandards, getStandardsItem, listAreas, getArea]
generated: '2026-08-10'
method: generated
source: openapi/apievangelist-v1-openapi.yml
---

# Map the vendor landscape for a capability

Use this to answer "who is in this space and who is actually being used" without falling back on
a vendor's own marketing.

## Before you start

- Base URL `https://api.apievangelist.com/v1`, keyless.
- Two distinct registries: `solutions` (~740 commercial third-party API services and tools) and
  `tools` (~400 open-source tools in use across the companies API Evangelist tracks). Do not
  merge them — one is a buy, the other is a build.
- Adoption counts come from the Insights side (`/insights/adoption`) and are demand-side signal,
  not vendor claims.

## Steps

1. **Anchor on the area.** `listAreas` — `GET /areas?q=<capability>` — then `getArea`. The area
   page is the editorial frame for the capability and tells you the vocabulary the rest of the
   network uses for it.
2. **List the commercial field.** `listSolutions` —
   `GET /solutions?q=<capability>&limit=50`. Read `meta.total` before paginating.
3. **List the open-source field.** `listTools` — `GET /tools?q=<capability>&limit=50`.
4. **Rank by real adoption, not by listing order.** `listInsightAdoption` —
   `GET /insights/adoption?type=solutions` (and `tools`, and `standards`) ranks by how many
   profiled companies adopt each one. This is the step that separates this from a directory dump.
5. **Pull detail on the shortlist.** `getSolution` (`GET /solutions/{slug}`) and `getTool`
   (`GET /tools/{slug}`) give the website and adoption count for one entry.
6. **Check the interoperability floor.** `listStandards` / `getStandardsItem` — if the capability
   has a standard, a vendor that does not implement it is a lock-in decision, and should be
   presented as one.

## Error handling

- `404 not_found` — a solutions slug is not a tools slug. Confirm which registry the entry came
  from before fetching detail.
- `403 upgrade_required` — some Insights depth is Pro (`getCompanyGaps`, `/stats`). The adoption
  ranking used above is free.
- No `429` or `5xx` declared. Pace at well under 5 req/s when paginating two registries.

## Conventions that apply

- `page` + `limit` (max 100); `fields=name,slug,url` trims the payload substantially when you are
  only building a shortlist.
- All `GET`; retries are safe.
- Errors are `{error, detail}` JSON, not RFC 9457.

See `conventions/api-evangelist-conventions.yml`.
