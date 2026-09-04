---
name: Embed a VICE article with oEmbed
description: Turn any VICE permalink into a conformant oEmbed 1.0 rich response using VICE's own oEmbed provider endpoint, with the failure mode that catches most callers.
api: openapi/_ae-authored/vice-media-wp-rest-openapi.yml
operations:
  - get_oembed_1_0_embed
  - get_wp_v2_posts
---

# Embed a VICE article with oEmbed

VICE runs a real oEmbed 1.0 provider endpoint. If your system already speaks oEmbed you need no
VICE-specific connector at all — this is the one place VICE conforms to its own industry's
standard.

## The call — `get_oembed_1_0_embed`

```
GET https://www.vice.com/wp-json/oembed/1.0/embed?url=<url-encoded article permalink>
```

Optional: `format` (`json` — the default — or `xml`), `maxwidth`, `maxheight`.

A 200 returns a conformant oEmbed 1.0 rich response:

```json
{
  "version": "1.0",
  "provider_name": "VICE",
  "provider_url": "https://www.vice.com",
  "author_name": "…",
  "title": "…",
  "type": "rich",
  "width": 600,
  "height": 338,
  "html": "<blockquote class=\"wp-embedded-content\">…"
}
```

## The failure mode

**`url` must be a permalink to a single post or page. The site root is not one.**

```
GET /wp-json/oembed/1.0/embed?url=https://www.vice.com/
→ 404 {"code":"oembed_invalid_url","message":"Not Found","data":{"status":404}}
```

That is the same 404 you get for a genuinely missing article, so do not treat
`oembed_invalid_url` as "this article does not exist" — check the shape of the URL first.

## Getting a valid permalink

Every object from `get_wp_v2_posts` carries `link`, which is exactly what the oEmbed endpoint
wants:

```
GET https://www.vice.com/wp-json/wp/v2/posts?search=<terms>&per_page=5&_fields=id,title,link
```

Then URL-encode that `link` into the `url` parameter.

## Discovery

VICE also advertises the surface itself. Every page carries
`<link rel="https://api.w.org/" href="https://www.vice.com/wp-json/" />` in its head, and
`https://www.vice.com/robots.txt` disallows nothing. `video.vice.com` runs a second install and
advertises its own `/wp-json/` the same way — but its public archive is effectively empty
(`X-WP-Total: 1`), so do not route embed lookups there.

## No credential, no limit signal

The endpoint is anonymous. No rate-limit header of any kind is returned, and none is documented,
so cache what you resolve rather than re-resolving per render.
