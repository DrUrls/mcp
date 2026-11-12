# DrUrls: website SEO audits

Use the `drurls` tools when the user asks about a website's SEO, why a site or page is not indexed by Google, what to fix first on a site, or wants a site audited or a report written.

- **No account needed** for one page: `free_page_check` with a public URL.
- **The user's sites:** `list_sites` first, then `get_site_report`, `find_issues` or `check_google_visibility` for one domain.
- **What to fix first:** `get_improvement_plan` (uses credits; say so before calling it).
- **A new audit:** `start_scan` starts it (uses a credit), and `get_scan_status` follows it. An audit takes a few minutes; do not poll in a tight loop.
- **A report to share:** `generate_report`.

Signing in happens through OAuth the first time a tool needs the user's data. Quota and credit errors come back as data: relay them, do not retry.
