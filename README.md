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

Vice Media is the Brooklyn, New York youth-culture and news media company founded in 1994 in Montreal,
which filed for Chapter 11 in May 2023 and was acquired for $350 million by a consortium led by Fortress
Investment Group. It operates through Vice Studios Group, Vice TV, the Virtue creative agency and Vice
Digital.

## What this profile found

**Vice Media runs no developer programme.** There is no developer portal, no API reference, no getting
started guide, no SDK, no CLI, no API pricing and no developer support channel. Searching for one and
finding nothing is a finding, and it is recorded as `x-api-posture: no-product-api`.

What does exist is a real, live, anonymously readable HTTP contract, and the company advertises it
itself:

- **`https://www.vice.com/wp-json/`** — a WordPress REST route-discovery document declaring **601
  routes**, linked from the head of every page on the site as
  `<link rel="https://api.w.org/" href="https://www.vice.com/wp-json/" />`, with a `robots.txt` that
  disallows nothing. The `wp/v2` content namespaces read with **no credential at all**: the collection
  returns `X-WP-Total: 822047` across 20 language editions.
- **`https://video.vice.com/wp-json/`** — a second install, 586 routes, the same shape, and an
  effectively empty public archive (`X-WP-Total: 1`). A live contract with nothing behind it.
- **`https://api.vice.com/`** — a credential-gated platform gateway. Every anonymous request, including
  a control path that cannot exist, returned the identical
  `{"message":"No client found attached to request","code":"invalid_req_client","status":401}` from a
  service identifying itself as `x-app-version: api-auth 1.13.2`. Nothing about its contract is
  observable without a client credential, so nothing about it is asserted.

`openapi/_ae-authored/vice-media-wp-rest-openapi.yml` (178 paths, **379 operations**) and its video
sibling (160 paths, 349 operations) are **derived by API Evangelist**, mechanically and verbatim, from
those route-discovery documents — which are saved next to them unmodified. Vice Media publishes no
OpenAPI of its own.

## Who actually operates the surface

vice.com's own About page states it is **"owned and operated by VICE Digital Publishing, LLC a Savage
Ventures company"** (Nashville, TN). That is the joint venture Vice Media formed with Savage Ventures in
2024, in which Vice Media retained brand control; the `savage/v1` and `savage-platform/v1` namespaces in
the route document are that operator's plugins. The surfaces are catalogued here because vice.com is the
VICE brand's own domain, and the operator relationship is recorded in `x-operator` rather than glossed
over. Content licensing and pitches route to `savage.ventures` addresses; press, advertising and security
remain on `vice.com`.

## Two things worth knowing before building on it

1. **Authorship is a taxonomy, not a user.** `/wp/v2/users` returns 401, and so does the
   `byline-manager/v1` namespace that would resolve a byline to a contributor. What reads anonymously is
   the `byline` taxonomy itself. The same is true of `/wp/v2/comments`, `/wp/v2/settings`, the
   ElasticPress facets and the WordPress Abilities registry — all 401.
2. **Do not walk 822,047 posts by page number.** WordPress refuses deep offsets at that size. Partition
   by year, by `platform-languages` term, or by category — every taxonomy term carries a `count`, so you
   can size a slice before fetching it.

## Standards it does speak

A conformant **oEmbed 1.0** provider endpoint (`provider_name: "VICE"`), **RSS 2.0** with Dublin Core,
Atom, slash and Yahoo Media RSS namespaces, a **sitemaps.org 0.9** index partitioned by year back to
1970, RFC 8288 `Link` pagination, and schema.org JSON-LD on article pages. For a publisher, that is the
set that matters — an integrator who already speaks oEmbed and RSS needs no VICE-specific connector.

What it does not: no `/.well-known/` document of any kind on any host, no `apis.json`, no OAuth or OIDC
metadata, no RFC 9457 problem details, no agent card, and no MCP server.

## Access posture and security

`https://www.vice.com/robots.txt` carries `User-agent: * / Disallow:` — nothing is disallowed, and no
Content Signals policy or AI-crawler rule is declared. The file is otherwise a Yoast-generated sitemap
list.

VICE publishes a substantive **responsible-disclosure policy** at
https://www.vice.com/en/vice-responsible-disclosure-policy/ — `infosec@vice.com`, PGP available, explicit
safe-harbor language, and a clear statement that no bounty is paid. It is linked from the footer of every
page but is **not** served at `/.well-known/security.txt`, which returns 404. Publishing those few lines
at the RFC 9116 path is the single cheapest improvement available to this provider.

`vicemediagroup.com` serves an **expired TLS certificate** (observed 2026-09-04); the `www.` form
redirects to `www.vicemedia.com` and is fine. `www.vice.com` sets no HSTS header, though `api.vice.com`
does.
