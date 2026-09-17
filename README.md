# FCC Filing Agent Kit

> **⚠️ Not legal advice.** This kit, and anything produced with it, was not created by a
> lawyer or anyone with legal training or a legal background. It is AI-assisted research
> and drafting tooling, nothing more. AI makes mistakes — it can misstate the law, miscite
> authority, misjudge procedural posture, or miss controlling precedent entirely, sometimes
> confidently and without any obvious sign of error. Nothing produced using this kit should
> be filed with the FCC, relied upon, or treated as correct until it has been fully
> reviewed by a licensed attorney qualified in FCC/communications law. Treat every draft
> this kit helps produce as a starting point for that attorney's review, never as a
> finished legal document.

A reusable starting point for preparing an FCC filing (Petition for Rulemaking, Petition
for Reconsideration, Comment/Reply Comment, Request for Waiver, etc.) with AI research
assistance, generalized from the process used to prepare the
[`fcc-special-event-call-sign-petition`](https://github.com/Reid-n0rc/fcc-special-event-call-sign-petition)
draft petition.

## What's in here

- [`AGENTS.md`](./AGENTS.md) — the persona, research standards, ECFS research workflow, and
  repository conventions any agent (human or AI) should follow when preparing a new filing.
  Read this first.
- [`FORMATTING.md`](./FORMATTING.md) — the legal formatting requirements a filing must meet
  (47 C.F.R. § 1.49 paper/type/spacing rules, content requirements by filing type), kept
  independent of any specific rendering tool.
- [`CLAUDE.md`](./CLAUDE.md) — loads `AGENTS.md` automatically for Claude Code sessions
  opened in a repo copied from this kit.
- [`.mcp.json`](./.mcp.json) — configures the `mcp-fcc-ecfs` MCP server for searching the
  FCC's Electronic Comment Filing System (ECFS). See **About `mcp-fcc-ecfs`** below before
  relying on it.

## How to use this kit

1. Copy this directory to a new repository for the specific filing you're preparing (or
   copy just `AGENTS.md`, `FORMATTING.md`, `CLAUDE.md`, and `.mcp.json` into an existing
   one).
2. Fill in the **"Filing-specific fields to fill in when starting a new project"** section
   at the bottom of `AGENTS.md` with the type of filing, the rule/docket at issue, the
   petitioner's identity, and a one-paragraph statement of the request.
3. Create a `sources/` directory (with its own `README.md` indexing what's in it) as
   primary-source research accumulates.
4. Start drafting the filing itself as a Markdown file (e.g. `PETITION.md` or
   `COMMENTS.md`) — the single source of truth, per `AGENTS.md`'s repository conventions.
5. Follow the review-before-push workflow in `AGENTS.md`: make edits, verify citations and
   formatting, show the diff to the human petitioner, and only commit/push after explicit
   approval.

## About `mcp-fcc-ecfs`

`.mcp.json` in this kit points Claude Code at the community
[`pipeworx-io/mcp-fcc-ecfs`](https://github.com/pipeworx-io/mcp-fcc-ecfs) MCP server, which
exposes ECFS search as MCP tools (`ecfs_search_filings`, `ecfs_docket_filings`,
`ecfs_filing_detail`, `ecfs_search_proceedings`).

**This is a third-party, community-maintained server, not an official FCC tool**, and as of
this kit's creation it has very little track record (a newly created repository, no
meaningful stars/forks history). It works by proxying your queries through its own hosted
gateway (`gateway.pipeworx.io`) rather than running locally or talking to the FCC directly.
Two things follow from that:

1. **Verify, don't just cite.** Treat anything it returns as a lead to the real filing, not
   a citable source in itself — confirm the actual filing text (via `ecfs_filing_detail` or
   by downloading the underlying PDF from `fcc.gov`/`docs.fcc.gov`) before citing it in a
   filing meant to go to the Commission. `AGENTS.md` already directs this.
2. **If you'd rather not route queries through a third-party gateway**, remove
   `.mcp.json` (or its `fcc-ecfs` entry) and use the fallback methods documented in
   `AGENTS.md`'s ECFS research workflow instead: the official ECFS Public API
   (`https://publicapi.fcc.gov/ecfs/`, free API key required — register at
   `https://www.fcc.gov/ecfs/help/public_api`), or browser automation against the ECFS web
   UI at `fcc.gov/ecfs/search`.
