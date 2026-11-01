# Vice Media

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Vice Media is the Brooklyn, New York youth-culture and news media company founded in 1994 in Montreal by Suroosh Alvi, Shane Smith and Gavin McInnes, which grew from the VICE magazine into a global multi-platform publisher, film and television studio and creative agency before filing for Chapter 11 in May 2023 and being acquired for $350 million by a consortium led by Fortress Investment Group. It operates today through Vice Studios Group, Vice TV, the Virtue creative agency and Vice Digital. Vice Media runs no developer programme, publishes no API documentation, portal, SDK or pricing, and sells no API product. It is catalogued here because its flagship editorial property, vice.com — owned and operated under the VICE brand by VICE Digital Publishing, LLC, the Savage Ventures joint venture Vice Media announced in 2024 — serves a live, anonymously readable WordPress REST API of 601 routes that the site advertises in the head of every page, exposing an editorial archive of 822,047 posts across 20 language editions, plus an oEmbed 1.0 provider endpoint and RSS 2.0 syndication. A second WordPress install answers on video.vice.com, and a separate authenticated platform gateway on api.vice.com answers every anonymous request with HTTP 401.

**Areas:** Company · Media · Publishing · News · Digital Media · Content · Video · Entertainment · WordPress · Syndication · oEmbed · Brooklyn

## Vice Media on APIs.io

Everything profiled for Vice Media is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/vice-media/](https://apis.io/providers/vice-media/)** — or go straight to one of the APIs or properties below.

### APIs (6)

- [VICE Platform API](https://apis.io/apis/vice-media/vice-media-platform-api/) — An authenticated platform gateway on api.vice.com, running nginx in front of an Express service that identifies itself as "api-auth 1.13.2" in the…
- [Vice Media Website (WordPress REST)](https://apis.io/apis/vice-media/vice-com-website-wordpress-rest/) — The public WordPress REST API (wp-json) of the Vice Media website at www.vice.com: the route index of the site's content management system, catalogued as…
- [Vice Media Oembed/1.0 API](https://apis.io/apis/vice-media/vice-media-oembed-1-0-api/) — oEmbed 1.0 provider endpoints — discovery and proxy for embeddable representations of VICE articles and videos.
- [Vice Media Root API](https://apis.io/apis/vice-media/vice-media-root-api/) — REST API index / namespace and route discovery.
- [Vice Media Wp Abilities/v1 API](https://apis.io/apis/vice-media/vice-media-wp-abilities-v1-api/) — WordPress Abilities API — the registry of named abilities an agent can discover and run. Read and run are capability-gated (observed HTTP 401 anonymously).
- [Vice Media Wp/v2 API](https://apis.io/apis/vice-media/vice-media-wp-v2-api/) — WordPress core content API — posts, pages, media, custom post types (sections, profiles, products), taxonomies (categories, tags, bylines, brands, platform…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [vice-media-mcp.yml](https://apis.io/servers/vice-media/vice-media-mcp-yml/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Vice Media Video Wp Rest Overlay](https://apis.io/overlays/vice-media/vice-media-video-wp-rest-overlay/)
- [Vice Media Wp Rest Overlay](https://apis.io/overlays/vice-media/vice-media-wp-rest-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Vice Media Authentication](https://apis.io/security/vice-media/vice-media-authentication/)
- [Vice Media Domain Security](https://apis.io/security/vice-media/vice-media-domain-security/)
- [Vice Media Vulnerability Disclosure](https://apis.io/security/vice-media/vice-media-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Vice Media Plans Pricing](https://apis.io/plans/vice-media/vice-media-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Vice Media Rate Limits](https://apis.io/rate-limits/vice-media/vice-media-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.vice.com/)
- [Pricing](https://www.vice.com/en/section/membership/)
- [Sign up](https://www.vice.com/en/section/membership/)
- [Blog](https://www.vice.com/en/)
- [Security](https://www.vice.com/en/vice-responsible-disclosure-policy/)
- [Terms of service](https://www.vice.com/en/terms/)
- [Privacy policy](https://www.vice.com/en/privacy/)
- [GitHub](https://github.com/VICEMedia)

## API Evangelist rating

**Kin Score 36.6** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 69.6 |
| Contract quality | 15.0 |
| Contract governance | 18.2 |
| Operational transparency | 13.2 |
| Developer ergonomics | 25.6 |
| Access clarity | 76.3 |

**Agent readiness 19.6** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 30.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/vice-media/](https://apis.io/providers/vice-media/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Vice Media: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/vice-media/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
