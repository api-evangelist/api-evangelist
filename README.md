# API Evangelist (api-evangelist)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This one *is* our API.** Almost every repository in this network is an independent, third-party
> profile of some other company's public API surface. This one is not. API Evangelist is profiling
> itself, in the same directory, against the same rubric, with the same checks — because a rating
> system nobody will point at their own work is a sales instrument, not a measurement.
>
> **Where the information came from.** The same place it comes from for everyone else: material a
> member of the public can reach with a browser and no credentials — the developer portal at
> [developer.apievangelist.com](https://developer.apievangelist.com), the OpenAPI definitions
> published there, the MCP server card, `llms.txt`, the agent skills, and the public feeds behind
> each network collection. First-party knowledge was **not** used to fill gaps that the public
> surface does not actually expose. Where a pointer did not resolve, it was removed rather than
> carried forward — see `x-evidence` in [`apis.yml`](apis.yml).
>
> **The rating is the same rating.** The Kin Score and Agent Readiness numbers on this profile are
> produced by the same engine, from the same `scoring.yml`, as every other provider in the catalog.
> No exemption, no manual adjustment, no rounding in our favor. If the score is low, that is the
> finding.
>
> **Corrections are still free, and still welcome.** If this profile misrepresents the API
> Evangelist API surface — or if you think the rubric is scoring it wrongly — open an issue on this
> repository or email [info@apievangelist.com](mailto:info@apievangelist.com). Criticism of our own
> listing gets the same treatment as criticism of anyone else's.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The index of everything available via the API Evangelist developer portal at
developer.apievangelist.com — sixteen years of API research served as one REST API, an MCP server
for agents, a governance and discovery compute layer, and the static JSON feeds behind each network
collection.

## APIs

| API | Base URL | Contract |
| --- | --- | --- |
| API Evangelist Network API | `https://api.apievangelist.com/v1` | [`openapi/apievangelist-v1-openapi.yml`](openapi/apievangelist-v1-openapi.yml) |
| API Evangelist Governance & Discovery API | `https://api.apievangelist.com/v1` | [`openapi/apievangelist-governance-openapi.json`](openapi/apievangelist-governance-openapi.json) |
| API Evangelist MCP Server | `https://mcp.apievangelist.com/mcp` | [server card](https://apievangelist.com/.well-known/mcp/server-card.json) |

Plus the network collection feeds — posts, areas, guidance, rules, policies, standards, strategies,
schema, properties, experiences, conversations, vocabularies, companies, apis, and more. The full
set, with pointers, is in [`apis.yml`](apis.yml).

## Agent surface

- **MCP server** — `https://mcp.apievangelist.com/mcp` (Streamable HTTP)
- **Server card** — `https://apievangelist.com/.well-known/mcp/server-card.json`
- **Agent skills** — `https://apievangelist.com/skills/`
- **llms.txt** — `https://apievangelist.com/llms.txt`

## Access

Free tier is keyless (5 req/s, 1,000 req/day). Higher limits and the Pro research content require a
key — see [developer.apievangelist.com/plans](https://developer.apievangelist.com/plans/).
