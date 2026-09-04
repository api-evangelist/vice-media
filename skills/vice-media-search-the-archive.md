---
name: Search the VICE editorial archive
description: Query VICE's 822,047-post editorial archive over the public WordPress REST API — free text, date range, category, tag, byline and language edition — and fetch a single article with its author, image and terms in one round trip.
api: openapi/_ae-authored/vice-media-wp-rest-openapi.yml
operations:
  - get_wp_v2_posts
  - get_wp_v2_posts_by_id
  - get_wp_v2_search
---

# Search the VICE editorial archive

VICE serves its editorial archive over an unauthenticated WordPress REST API at
`https://www.vice.com/wp-json`. There is no key, no signup and no plan. There is also no
published rate limit and no rate-limit header, so pace yourself — see
`rate-limits/vice-media-rate-limits.yml`.

## Authentication

None. Send no credential. Adding one changes nothing: the write surface needs a WordPress
application password that third parties cannot obtain.

## 1. Search the archive — `get_wp_v2_posts`

```
GET https://www.vice.com/wp-json/wp/v2/posts?search=<terms>&per_page=20&orderby=relevance
```

Parameters that matter, all declared in the contract:

| Parameter | Notes |
|---|---|
| `search` | free text |
| `search_columns` | narrow to `post_title`, `post_content`, `post_excerpt` |
| `search_semantics` | `exact` for literal matching |
| `after` / `before` | ISO 8601 publish-date bounds |
| `modified_after` / `modified_before` | ISO 8601 update bounds |
| `categories` / `tags` / `categories_exclude` / `tags_exclude` | term ids, not slugs |
| `slug` | array of post slugs |
| `orderby` | `date` (default), `relevance`, `modified`, `title`, `id`, `include` |
| `order` | `asc` / `desc` |
| `per_page` | 1–100, default 10 |
| `page` | 1-based |

Two non-contract parameters that work and are worth using — both confirmed live:

- `_fields=id,title,link,date` — sparse response. Cuts a page of results from ~13 KB to a few
  hundred bytes.
- `_embed=1` — inlines `_embedded.author`, `_embedded["wp:featuredmedia"]` and
  `_embedded["wp:term"]` instead of making you follow `_links`.

## 2. Read the pagination signal

Every collection response carries:

- `X-WP-Total` — total matching items
- `X-WP-TotalPages` — total pages at the current `per_page`
- `Link: <…&page=2>; rel="next"` (RFC 8288)

All three are named in `Access-Control-Expose-Headers`, so they are readable from a browser too.

**Do not try to walk the whole archive by page number.** `X-WP-Total` on the unfiltered
collection is 822,047. WordPress refuses deep offsets on collections that size. Partition the
work instead — by year (`after`/`before`), by language edition, or by category.

## 3. Fetch one article — `get_wp_v2_posts_by_id`

```
GET https://www.vice.com/wp-json/wp/v2/posts/{id}?_embed=1
```

`id` is a site-local integer. There are no prefixed or opaque identifiers.

## 4. Cross-type search — `get_wp_v2_search`

```
GET https://www.vice.com/wp-json/wp/v2/search?search=<terms>
```

Returns a flat list of `{id, title, url, type, subtype}` across posts, pages and terms. Use it
when you do not know which content type holds the thing you are looking for; use
`get_wp_v2_posts` when you do, because it returns full objects.

## Errors

Errors are **not** RFC 9457. The envelope is:

```json
{"code": "rest_forbidden", "message": "Sorry, you are not allowed to do that.", "data": {"status": 401}}
```

- `401 rest_forbidden` — you asked for something closed. Do not retry with a credential; you
  cannot get one. Closed collections include `/wp/v2/users`, `/wp/v2/comments`,
  `/wp/v2/settings` and every editorial plugin namespace.
- `404 rest_no_route` — bad path. `GET /wp-json/` returns the live route list.
- `400 rest_invalid_param` — check `data.params` for which argument was rejected.

Full catalog: `errors/vice-media-problem-types.yml`.

## What you cannot do

Resolve `post.author` to a person. Authorship on this site is a **taxonomy** (`byline`), not the
WordPress user record — `/wp/v2/users` returns 401. Read `byline` terms instead; see the
companion skill.
