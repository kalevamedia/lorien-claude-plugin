---
name: lorien-publishing-flow
description: Use when the user asks how content is published in Lorien, about the content model (assets, versions, publish decisions), content visibility, channels, sections, or why an item isn't showing up on the Delivery API. Says which portal pages to read before answering.
---

# Publishing in Lorien: read these pages first

The Lorien content model and the rules that decide what the Delivery API serves are documented on the developer portal. Fetch them before answering; do not reconstruct them from memory.

| Question | Find the page with |
|----------|--------------------|
| What are publishers, channels, assets, versions and publish decisions? | `lorien_docs_search("content model")` |
| Why doesn't an item appear on the Delivery API? | `lorien_docs_search("content visibility")` |
| How do I create, version and publish content through the Management API? | `lorien_docs_search("asset lifecycle")`, then `lorien_docs_search("creating articles")` |
| Idempotent imports, concurrency, retries | `lorien_docs_search("integration patterns")` |

Fetch the top hit of each with `lorien_docs_get_page`.

The one thing worth knowing before fetching: marking a version ready does not publish it. Publishing is a separate, explicit publish decision per channel, and the visibility page lists every rule that gates delivery. When a user reports "it's ready in the Management API but not on the Delivery API", walk through those rules in order with the page open.

When the user wants code, fetch the guide and the matching reference page, then use the documented request and response shapes verbatim.
