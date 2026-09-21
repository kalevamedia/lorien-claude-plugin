# lorien-claude-plugin

Claude Code plugin for the Lorien developer portal at https://developers.loriencms.com. It gives Claude Code three MCP tools for searching and reading the portal's documentation, plus three skills that tell Claude how to use them.

## Prerequisites

- Claude Code 2.1.121 or newer (check with `claude --version`).
- A Lorien developer-portal account, the same one you use at https://developers.loriencms.com. Accounts are issued by the Lorien team; ask your Lorien contact at Kaleva Media if you don't have one.
- Port 33418 free on localhost. Claude Code listens there for the sign-in callback.

## Install

The repo doubles as a single-plugin Claude Code marketplace. In a Claude Code session, run:

```
/plugin marketplace add kalevamedia/lorien-claude-plugin
/plugin install lorien-claude-plugin@lorien
```

Run `/reload-plugins` afterwards. `/help` should now list the three skills under the `lorien-claude-plugin:` namespace.

## First sign-in

The first time Claude Code calls a Lorien tool, it opens your browser to sign in with your developer-portal account. Sign in, return to the terminal, and the original tool call proceeds. The access token is cached for two hours and refreshed transparently after that. If the refresh fails, for example because you signed out of the portal, you are prompted to sign in again.

## Try it

- "Search the Lorien docs for content visibility."
- "How do I authenticate to the Lorien Delivery API? Use the Lorien docs."
- "List the Lorien Delivery API reference pages."

## Troubleshooting

- **Browser doesn't open, or the callback never returns.** Something else is listening on port 33418. Free it (`lsof -nP -iTCP:33418`) and retry.
- **Repeated 401 errors.** The refresh token has expired. Open `/mcp`, pick the Lorien server, and re-authenticate.
- **Tools are never invoked.** Make the lookup explicit: "using the Lorien docs, …" or "search the Lorien developer portal for …".

Full documentation, including the tool reference and worked prompts, is on the portal under `/docs/plugin` after sign-in.

## Uninstall

```
/plugin uninstall lorien-claude-plugin@lorien
/plugin marketplace remove lorien
```

## Support

Open an issue in this repository for problems with the plugin. For portal accounts, API credentials, and anything security-related, contact your Lorien contact at Kaleva Media rather than filing a public issue.

## License

Apache-2.0. See [LICENSE](LICENSE).
