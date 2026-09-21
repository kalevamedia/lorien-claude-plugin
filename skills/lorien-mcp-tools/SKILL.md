---
name: lorien-mcp-tools
description: Use whenever you need to look up Lorien documentation, find API operations, or fetch a specific docs page. Tells you which MCP tool to use, in what order, and with what arguments.
---

# Lorien MCP tools — how to use them

The plugin exposes three MCP tools that search and fetch pages from the Lorien developer portal at https://developers.loriencms.com. Claude Code lists them as `docs-tools___lorien_docs_search` and so on; this skill uses the short names.

## Tool reference

### `lorien_docs_search(query, limit=10)`

Free-text search across the entire portal. Use it first when you don't know which page is most relevant.

Returns `{ query, hits: [{ slug, title, snippet, url }], count }`. The `slug` is what you pass to `lorien_docs_get_page`.

Tips:
- Phrase queries the way a developer would search — verbs and nouns, not full sentences. "list channels", "authentication", "image versioning".
- Defaults to 10 hits; ask for more with `limit` up to 25.

### `lorien_docs_get_page(slug)`

Fetch one full page as markdown. Pass a slug exactly as a search hit or a listing returned it. Returns `{ slug, title, url, body_markdown }`.

Tips:
- Do not guess slugs. Get them from `lorien_docs_search` or `lorien_docs_list_pages`.
- Pass the slug as returned: no leading `docs/`, no `.md` suffix. A leading `docs/` is stripped, but a `.md` suffix is not and yields "page not found".
- Auto-generated API reference pages (slugs containing `/reference/`) can run to tens of thousands of tokens. Summarise rather than paste them back to the user.

### `lorien_docs_list_pages(prefix="")`

List pages on the portal, optionally filtered by slug prefix. Returns `{ prefix, pages: [{ slug, title, summary }], count }`.

Tips:
- Use when the user wants to browse what exists ("what's documented about the Management API?"). Take the prefix from the first path segment of a search hit's slug.
- The listing is capped at 200 pages, sorted by slug. When more matched, the result also carries `total`, `truncated: true` and a `note`; narrow with a longer prefix. An empty prefix stops partway through the alphabet and does not reveal every section, so it is not a way to see the whole portal.

## Recommended call sequences

| Goal | Tools, in order |
|------|------------------|
| "Find the page about X" | `lorien_docs_search` → maybe `lorien_docs_get_page` on top hit |
| "Summarise page X for me" | `lorien_docs_get_page` directly if you already have the slug |
| "What's documented under X area?" | `lorien_docs_search` for X to get a slug, then `lorien_docs_list_pages` with that slug's first path segment |
| "Write integration code for X" | `lorien_docs_search` for X, then `lorien_docs_get_page` on the guide and the reference page, then write |

## Authentication

The MCP server requires signing in with a Lorien developer-portal account. The first tool call in a fresh session opens a browser; sign in, return to the terminal, and the access token is cached for two hours. Claude Code refreshes it transparently after that. If the refresh fails, for example after signing out of the portal, it prompts for sign-in again.

If the user has no account yet, accounts are issued by the Lorien team: tell them to ask their Lorien contact at Kaleva Media. Sign-up on the portal is restricted and needs manual approval.
