---
name: Walk VICE editions, sections and bylines
description: Enumerate VICE's 20 language editions, editorial sections, categories and contributor bylines from the public WordPress REST API, and use their term counts to size the archive before querying it.
api: openapi/_ae-authored/vice-media-wp-rest-openapi.yml
operations:
  - get_wp_v2_platform_languages
  - get_wp_v2_categories
  - get_wp_v2_byline
  - get_wp_v2_vice_section
  - get_wp_v2_taxonomies
  - get_wp_v2_types
---

# Walk VICE editions, sections and bylines

VICE registers taxonomies a stock WordPress site does not. Read them first: every term carries a
`count`, so the taxonomy endpoints tell you how big a slice is *before* you fetch any of it.

All of these read anonymously. No credential.

## 1. Discover what this install actually registers

```
GET https://www.vice.com/wp-json/wp/v2/types        # get_wp_v2_types
GET https://www.vice.com/wp-json/wp/v2/taxonomies   # get_wp_v2_taxonomies
```

Do this rather than assuming. The VICE-specific entries are:

- **Post types**: `vice_section` (Sections), `profile` (contributor profiles), `sp_product`
  (membership and magazine products)
- **Taxonomies**: `byline` (authorship), `sp_language` (the edition split, `rest_base`
  `platform-languages`), `sp_brand` (`rest_base` `brands`)

## 2. Size the editions — `get_wp_v2_platform_languages`

```
GET https://www.vice.com/wp-json/wp/v2/platform-languages?per_page=100
```

Twenty language editions share one post collection. Each term returns `{id, name, slug, count,
link}` — `count` is that edition's archive size. Then filter posts with the term id.

## 3. Sections and categories

```
GET https://www.vice.com/wp-json/wp/v2/vice_section?per_page=100   # get_wp_v2_vice_section
GET https://www.vice.com/wp-json/wp/v2/categories?per_page=100     # get_wp_v2_categories
```

`vice_section` is a post type (the section landing pages: Pulse, Life, Tech, Munchies, Music,
Waypoint, Photography). `category` is the taxonomy that both posts and sections are filed under.
They are not the same axis — read both.

## 4. Bylines — `get_wp_v2_byline`

```
GET https://www.vice.com/wp-json/wp/v2/byline?per_page=100&orderby=count&order=desc
```

**This is how you get authorship on this site.** `/wp/v2/users` returns HTTP 401, and the
`byline-manager/v1` namespace that would resolve a byline term to a contributor profile is also
401. What reads is the taxonomy itself: term name, slug and `count` (pieces carried).

`get_wp_v2_profile` (`/wp/v2/profile`) reads anonymously too and holds the contributor profile
posts, but nothing public joins a `profile` to a `byline` term for you — match on name, and say
that the match is heuristic.

## 5. Filter posts by any term

Term ids, not slugs:

```
GET https://www.vice.com/wp-json/wp/v2/posts?categories=<id>&per_page=50&_fields=id,title,link,date
```

Read `X-WP-Total` off the response to confirm the slice size matches the term `count` you saw.

## Pagination

`per_page` maxes at 100 on every collection. `X-WP-Total` / `X-WP-TotalPages` /
`Link: rel="next"` are returned and CORS-exposed. Taxonomy collections are small enough to walk
end to end; the post collection is not.

## Errors

Same WordPress envelope as everywhere on this host — `{code, message, data.status}`, not RFC 9457.
A 401 here means the route is closed to the public, not that you need a better token.
