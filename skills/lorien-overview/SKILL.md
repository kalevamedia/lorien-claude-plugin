---
name: lorien-overview
description: Use when the user asks about Lorien, Kaleva Media's publishing platform, the developer portal, or any of the Lorien APIs (Delivery API, Management API, comments, reader personalisation). Orients Claude and says how to find the right portal pages before answering.
---

# Lorien in one paragraph

**Lorien** is Kaleva Media's B2B publishing platform. It runs Kaleva Media's own newspaper sites and is offered to other publishers. The developer portal at https://developers.loriencms.com is the canonical reference for the APIs integrators use. It requires a developer-portal account, and this plugin's tools read it on the user's behalf.

## The API surfaces

| API | Purpose |
|-----|---------|
| **Delivery API** | Read published content |
| **Management API** | Write side: create, version and publish content |
| **Comments API** | Comments and discussion threads attached to content |
| **Reader personalisation API** | Bookmarks, followed keywords, reading lists |

The portal has a section for each, plus general guides (getting started, authentication, pagination, caching, errors, rate limits). Search for the topic first; a hit's slug starts with its section's prefix, which `lorien_docs_list_pages` can then use to browse that section.

## How to answer Lorien questions

Do not answer from memory. Find the relevant portal page with `lorien_docs_search` (or `lorien_docs_list_pages`) and fetch it with `lorien_docs_get_page`; base the answer on it. Authentication details, base URLs, credentials and request shapes are documented on the portal and are environment-specific; the portal is the only source to quote.

- Authentication or credentials → search "getting started" (Delivery API) or "authentication" (Management API).
- Content model, channels, visibility → see the `lorien-publishing-flow` skill.
- Anything else → `lorien_docs_search`, then the top hit.

## What the plugin doesn't do (yet)

Live calls against the Lorien APIs. v1 is read-only documentation access; live tools are on the roadmap. When the user asks for something the plugin can't do, point them at the portal.
