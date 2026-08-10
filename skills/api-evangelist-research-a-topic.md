---
name: research-an-api-topic
description: Brief yourself on any API topic using the API Evangelist network — the matching topic area, the tag graph, the most recent stories, and (with a Pro key) the curated cross-network guide.
api: openapi/apievangelist-v1-openapi.yml
base_url: https://api.apievangelist.com/v1
auth: none required (keyless free tier); x-api-key for the Pro steps
operations: [searchNetwork, listAreas, getArea, getAreaRelated, listTags, getTag, listPosts, getPost, getPostRelated, getGuide]
generated: '2026-08-10'
method: generated
source: openapi/apievangelist-v1-openapi.yml
---

# Research an API topic

Use this when you need to get oriented on a topic (gateways, governance, agents, deprecation…)
before answering or writing about it.

## Before you start

- Base URL is `https://api.apievangelist.com/v1`. No key is needed for steps 1–5.
- Free tier is 5 requests/second and 1,000 requests/day. There is **no** `RateLimit` response
  header — pace yourself; the budget is not readable from the response.
- List responses are summaries. Add `include=content` to inline the markdown body (Pro on several
  collections).
- Paginate with `page` and `limit` (max `limit=100`), read `meta.total` and `meta.pages`.

## Steps

1. **Cast a wide net.** `searchNetwork` — `GET /search?q=<topic>&limit=10`. Read
   `meta.facets.types` first: it carries per-type hit counts for the **whole** result set, so it
   tells you where the topic actually lives before you read a single document.
2. **Narrow to the types that matter.** Re-run `searchNetwork` with
   `types=posts,guidance,rules` (comma-delimited) once the facets tell you which types are dense.
3. **Find the topic area.** `listAreas` — `GET /areas?q=<topic>` — then `getArea`
   (`GET /areas/{slug}`) for the one that matches. There are 77 areas and each one connects
   stories, building blocks, papers and services around a single topic.
4. **Walk the graph, do not re-search.** `getAreaRelated` (`GET /areas/{slug}/related`) gives you
   neighbouring areas; `getTag` (`GET /tags/{slug}`) resolves a tag to everything it labels across
   the whole network. Tags and `/related` are the only joins in this API — there are no id
   references between documents.
5. **Read the current writing.** `listPosts` — `GET /posts?q=<topic>&sort=date&limit=5` — then
   `getPost` (`GET /posts/{slug}`) with `include=content` on the two or three that matter. Post
   slugs are `YYYY-MM-DD-slug`; `getPostRelated` walks outward from any one of them.
6. **(Pro) Take the curated bundle instead.** `getGuide` — `GET /guide?topic=<topic>` — returns
   the matching area, top guidance/rules/policies/standards, papers, recent stories and the
   relevant services in one call. Requires `x-api-key`.

## Error handling

- `404 {"error":"not_found","detail":"posts <slug>"}` — the slug does not exist in that
  collection. List first and read `data[].slug`; do not guess slugs.
- `403 {"error":"upgrade_required","tier":"pro"}` — you hit a Pro operation (`/guide`, `/stats`,
  and `include=content` on some collections) without a key. Fall back to the free steps rather
  than retrying.
- `400 {"error":"bad_request"}` on `/guide` means `topic` is missing.
- `429` and `5xx` are **not** declared in the contract. If you get one, back off — there is no
  documented retry guidance.

## Conventions that apply

- No idempotency contract exists, but every operation here is a `GET`, so retries are safe.
- Errors are `application/json` `{error, detail}` — **not** RFC 9457, and there is no `type` URI
  to dereference.
- Responses carry `cache-control: public, max-age=300`; there is no `ETag`, so conditional
  requests are not available.

See `conventions/api-evangelist-conventions.yml` and `errors/api-evangelist-problem-types.yml`.
