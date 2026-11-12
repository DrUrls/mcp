# DrUrls MCP server

> Audit websites for SEO from Claude, ChatGPT, Cursor, VS Code, Gemini CLI and any MCP client: scores, every issue with its exact fix, and what blocks Google from indexing a site.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.drurls%2Fdrurls-blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.drurls)
[![Claude](https://img.shields.io/badge/Claude-connector-d97757)](https://claude.ai/directory/drurls)
[![ChatGPT](https://img.shields.io/badge/ChatGPT-plugin-10a37f)](https://chatgpt.com/plugins/plugin_asdk_app_6ae4cb7240388191b3906d56adc59406)
[![Add to Cursor](https://img.shields.io/badge/Cursor-Add_to_Cursor-black)](cursor://anysphere.cursor-deeplink/mcp/install?name=drurls&config=eyJ1cmwiOiJodHRwczovL2RydXJscy5jb20vbWNwIn0%3D)
[![Glama](https://img.shields.io/badge/Glama-listed-6b46c1)](https://glama.ai/mcp/connectors/com.drurls/drurls)

[DrUrls](https://drurls.com) crawls a website and ranks every SEO, performance, security and accessibility issue, with the fix for each. This server gives an AI assistant the same: list your sites, read their audits, check Google indexability, and start new audits.

- **Endpoint:** `https://drurls.com/mcp` (streamable HTTP, stateless)
- **Auth:** OAuth 2.1 with dynamic client registration: the client opens DrUrls, you sign in (Google, GitHub or an emailed link) and approve. Or send an API key as `Authorization: Bearer <key>`.
- **Registry name:** `com.drurls/drurls` ([server.json](server.json))

## What you can ask

- "Which of my sites has the worst SEO score, and why?"
- "What's stopping Google from indexing example.com?"
- "Give me the five fixes that would improve my site the most, with the exact change for each."
- "Run a fresh audit of example.com and tell me when it's done."
- "Check this page for SEO problems: https://example.com/pricing" (no account needed)
- "Write a client-ready SEO report for example.com."

## Connect

| Client | How |
|---|---|
| **Claude** (claude.ai, Desktop) | [Connect from Claude's directory](https://claude.ai/directory/drurls), or Settings → Connectors → Add custom connector → `https://drurls.com/mcp` |
| **ChatGPT** | [Open the DrUrls plugin](https://chatgpt.com/plugins/plugin_asdk_app_6ae4cb7240388191b3906d56adc59406) and connect |
| **Claude Code** | `claude mcp add --transport http drurls https://drurls.com/mcp`, then `/mcp` to sign in. Or the [plugin](https://github.com/DrUrls/claude-plugins): `/plugin marketplace add DrUrls/claude-plugins` |
| **Cursor** | [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=drurls&config=eyJ1cmwiOiJodHRwczovL2RydXJscy5jb20vbWNwIn0%3D), or `~/.cursor/mcp.json`: `{ "mcpServers": { "drurls": { "url": "https://drurls.com/mcp" } } }` |
| **VS Code** | `.vscode/mcp.json`: `{ "servers": { "drurls": { "type": "http", "url": "https://drurls.com/mcp" } } }` |
| **Gemini CLI** | `gemini extensions install https://github.com/DrUrls/mcp` (this repo is the extension: [gemini-extension.json](gemini-extension.json)) |
| **Codex** | `~/.codex/config.toml`: `[mcp_servers.drurls]` with `url = "https://drurls.com/mcp"` |
| **Windsurf** | `~/.codeium/windsurf/mcp_config.json`: `{ "mcpServers": { "drurls": { "serverUrl": "https://drurls.com/mcp" } } }` |
| **Any other client** | Streamable HTTP at `https://drurls.com/mcp`; OAuth is discovered from `/.well-known/oauth-protected-resource/mcp` |

Step by step: https://drurls.com/assistants

## Tools

Each tool's description states its current price; [drurls.com/pricing](https://drurls.com/pricing) is the rate card. Reading data your organization already has is free.

| Tool | What it does | Read-only |
|---|---|---|
| `list_sites` | Every site in your organization with its latest audit: score, grade, issues, pages crawled, last scan, and whether a scan is running. | ✅ |
| `get_site_report` | One site in depth: score, issue counts by severity, the most frequent issue types, social presence. | ✅ |
| `find_issues` | Open issues across all sites or one, filterable by severity, with affected-page counts. | ✅ |
| `check_google_visibility` | What blocks Google: noindex, robots blocks, sitemap errors, canonical problems, redirect chains, broken internal links. | ✅ |
| `get_improvement_plan` | The highest-impact fixes, ranked by severity and pages touched, with how to fix each. | |
| `start_scan` | Launch a fresh audit of a website (async; follow it with `get_scan_status`). | |
| `get_scan_status` | Scans in flight and the last 10 finished, with scores and errors. | ✅ |
| `generate_report` | A full report for one site or the whole organization. | |
| `free_page_check` | A single-page audit of any public URL. No account, no key. | ✅ |
| `list_tester_offers` | Tests a real person runs on a real device (mobile UX, checkout, screen reader, translation). | ✅ |
| `hire_tester` | Order one of those tests. | |

`initialize` and `tools/list` answer without auth, and `free_page_check` works with no account. Every other call needs OAuth or an API key; without one it gets `401` with a `WWW-Authenticate` challenge. Every tool carries a title and read-only / destructive / open-world annotations. In ChatGPT the two tester tools and all prices are hidden, per OpenAI's commerce rules.

## Security and privacy

- Approving a connection creates a key that works **only on the MCP endpoint**, with analyst rights: no team, billing or admin access. Revoke it any time from your DrUrls dashboard.
- Tools are scoped to your organization; nothing crosses to another account.
- No tool deletes anything. The tools that spend credits say so, and charge only when the call succeeds.
- Vulnerabilities: [security.txt](https://drurls.com/.well-known/security.txt) · Privacy policy: https://drurls.com/privacy

## FAQ

**How do I connect DrUrls to Claude?** From [Claude's directory](https://claude.ai/directory/drurls), or add `https://drurls.com/mcp` as a custom connector and sign in.

**Can I use it without an account?** Yes, for one page at a time: `free_page_check` audits any public URL. Your sites, history and full-site audits need a free account.

**Does it work with ChatGPT?** Yes, as a published plugin: [DrUrls for ChatGPT](https://chatgpt.com/plugins/plugin_asdk_app_6ae4cb7240388191b3906d56adc59406).

**What does it cost?** Reading your audits is free. Audits, plans and reports use credits from your plan's monthly allowance; each tool states its price.

**Is there a local (stdio) version?** No. It is a hosted remote server, so there is nothing to install or keep updated.

## Also from DrUrls

- **Chrome extension** (screenshots, screencasts, test flows): [Chrome Web Store](https://chromewebstore.google.com/detail/kcpconjhhkcfkkldojhljjfnhnejlpmb)
- **Dr Urls Sync** for VS Code: [Marketplace](https://marketplace.visualstudio.com/items?itemName=drurls.drurls-sync) · [Open VSX](https://open-vsx.org/extension/drurls/drurls-sync)

## Listed on

[Claude directory](https://claude.ai/directory/drurls) · [ChatGPT plugins](https://chatgpt.com/plugins/plugin_asdk_app_6ae4cb7240388191b3906d56adc59406) · [Official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.drurls) · [Glama](https://glama.ai/mcp/connectors/com.drurls/drurls) · [MCP Market](https://mcpmarket.com/server/drurls) · [Cursor Directory](https://cursor.directory/plugins/drurls) · [mcp.so](https://mcp.so/servers/drurls)

## Links

Docs: https://drurls.com/ai · Support: support@drurls.com · Changelog: [releases](https://github.com/DrUrls/mcp/releases)

This repository holds the server's public metadata. The server itself runs at drurls.com. MIT licence.

<!-- mcp-name: com.drurls/drurls -->
