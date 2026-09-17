# ECFS Research Workflow

Read this before searching for prior filings, orders, or comments in a docket — i.e. any
time `AGENTS.md`'s "Prior attempts and adverse authority get surfaced, not buried" standard
is actually being carried out.

The FCC's Electronic Comment Filing System (ECFS) is the primary way to find prior
petitions, comments, and orders in a docket, and to confirm no pending or resolved filing
already addresses the exact request being drafted.

- **Use the `mcp-fcc-ecfs` MCP server for ECFS searches** when it is configured in this
  environment (see `.mcp.json` / your MCP client config). It exposes tools such as
  `ecfs_search_filings` (full-text search), `ecfs_docket_filings` (list filings in a
  docket), `ecfs_filing_detail` (retrieve one filing by submission ID), and
  `ecfs_search_proceedings` (search dockets by number or query). Prefer these over ad hoc
  web scraping when they're available.
  - This is a third-party community MCP server, not an official FCC tool, and it proxies
    queries through its own hosted gateway rather than running locally. Treat anything it
    returns as a *lead*, not a verified citation: always confirm the actual filing text
    (via `ecfs_filing_detail`, or by downloading the underlying PDF) before citing it in
    the filing, the same as any other secondary source. If it is unavailable, misbehaves,
    or its results can't be cross-checked, fall back to the options below rather than
    stalling the research.
- **Fallback: the official ECFS Public API** (`https://publicapi.fcc.gov/ecfs/`),
  documented at `https://www.fcc.gov/ecfs/help/public_api`. Requires a free API key
  (register via the link on that page). Useful endpoints: `/filings` (search by
  `proceedings.name`, `q`, `date_received`, etc.), `/filing/{id_submission}`,
  `/proceedings`. Prefer `sort=date_received,ASC` when trying to find the earliest filing
  in a docket (i.e., what originally opened it).
- **Fallback: browser automation against the ECFS web UI** (`fcc.gov/ecfs/search/...`).
  Automated `curl`/`WebFetch`-style access to `fcc.gov` is commonly blocked by bot
  protection; a real browser session (e.g., Claude in Chrome) generally works where a bare
  HTTP client does not. This is slower and more manual than the API, but requires no key.
- **Always get the ECFS filing-detail permalink** (`https://www.fcc.gov/ecfs/search/
  search-filings/filing/<submission id>`) for anything cited that is itself an ECFS filing,
  and include it in the citation per `FORMATTING.md`'s citation conventions.
- When searching for "has anyone asked for this before," search by proceeding number *and*
  do a full-text search for the specific proposal — docket titles are often generic
  ("Amendment of Part XX Rules...") and won't surface a narrow request buried in someone
  else's comments. Read the order that resolved the docket, not just its title, to see
  whether it actually ruled on the specific point at issue.
