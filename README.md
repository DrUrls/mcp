# DrUrls MCP server

[DrUrls](https://drurls.com) audits websites for SEO. This MCP server lets an AI assistant list your sites, read their audits and the fix for each issue, check Google indexability, and start new audits.

**Endpoint:** `https://drurls.com/mcp` (streamable HTTP, stateless)
**Auth:** OAuth 2.1 with dynamic client registration — the client opens DrUrls, you sign in and approve. Or send an API key as `Authorization: Bearer <key>`.
**Registry name:** `com.drurls/drurls` ([server.json](server.json))

## Connect

| Client | How |
|---|---|
| Claude (claude.ai, Desktop) | [Connect from Claude's directory](https://claude.ai/directory/drurls), or Settings → Connectors → Add custom connector → `https://drurls.com/mcp` |
| ChatGPT | Add a custom connector (developer mode) with `https://drurls.com/mcp`, OAuth |
| Claude Code | `claude mcp add --transport http drurls https://drurls.com/mcp`, then `/mcp` to sign in — or the [plugin](https://github.com/DrUrls/claude-plugins) |
| Cursor | [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=drurls&config=eyJ1cmwiOiJodHRwczovL2RydXJscy5jb20vbWNwIn0%3D) ([Cursor Directory](https://cursor.directory/plugins/drurls)), or `~/.cursor/mcp.json`: `{ "mcpServers": { "drurls": { "url": "https://drurls.com/mcp" } } }` |
| VS Code | `.vscode/mcp.json`: `{ "servers": { "drurls": { "type": "http", "url": "https://drurls.com/mcp" } } }` |

Step by step: https://drurls.com/assistants

## Listed on

- [Claude connector directory](https://claude.ai/directory/drurls)
- [Official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.drurls): `com.drurls/drurls`
- [Glama](https://glama.ai/mcp/connectors/com.drurls/drurls)
- [Cursor Directory](https://cursor.directory/plugins/drurls)
- [mcp.so](https://mcp.so/servers/drurls)

The editor extension, **Dr Urls Sync**, is on the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=drurls.drurls-sync) and [Open VSX](https://open-vsx.org/extension/drurls/drurls-sync).

## Tools

Costs as of the last update of this file; each tool's description states its current price.

| Tool | What it does | Cost |
|---|---|---|
| `list_tester_offers` | Browse the catalogue of tests a real person will run on a real device: mobile UX on a handset, end-to-end checkout, a screen-reader pass by somebody who uses one daily, native-speaker translation review, and more. | free |
| `hire_tester` | Order one of the tests from list_tester_offers. | price of the offer |
| `list_sites` | List every site in the user's organization with its latest completed audit: SEO score, grade, issues found, pages crawled, when it was last scanned, and whether a scan is running right now. | free |
| `get_site_report` | Deep-dive one site: latest audit score, issue counts by severity, the most frequent issue types with counts, and social-network presence. | free |
| `find_issues` | Search open issues across all sites (or one site). | free |
| `check_google_visibility` | Check Google indexability for all sites (or one): noindex tags, robots blocks, sitemap errors, canonical problems, redirect chains and broken internal links found in the last crawl. | free |
| `get_improvement_plan` | The highest-impact actions to improve quality right now, ranked by severity and how many pages each fix touches, with concrete how-to-fix guidance. | 2 credits |
| `start_scan` | Launch a fresh audit of a website. | 1 credit |
| `get_scan_status` | What is running right now and what finished recently: every in-flight scan plus the last 10 completed/failed ones with scores and errors. | free |
| `generate_report` | Compile a full SEO report — for one site (score, issues by severity, top issue types, Google visibility, social presence, ranked fix plan) or the whole organization (per-site scores, visibility verdicts, top cross-site actions). | 2 credits |
| `free_page_check` | Free single-page SEO/health audit of any public URL — no API key, no account. | free |

`initialize` and `tools/list` answer without auth, and `free_page_check` works with no account. Every other call needs OAuth or an API key; a call without one gets `401` with a `WWW-Authenticate` challenge pointing at `/.well-known/oauth-protected-resource/mcp`. Every tool carries read-only / destructive / open-world annotations.

## Pricing

Usage is billed in credits from your plan's monthly allowance, then from credits you buy. Reading your own data is free; each paid tool states its price in its description. Plans: https://drurls.com/pricing

## Links

- Privacy policy: https://drurls.com/privacy
- Support: support@drurls.com
- MCP reference: https://drurls.com/ai

This repository holds the server's public metadata. The server itself runs at drurls.com.

MIT licence.
