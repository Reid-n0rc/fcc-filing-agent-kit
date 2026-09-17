# FCC Filing Formatting Requirements (47 C.F.R. § 1.49 and related rules)

This file states the *legal* formatting requirements that apply to documents filed with the
FCC, independent of whatever tool a given project uses to render the final PDF/document
(WeasyPrint, LaTeX, Word, etc.). When a new filing project's build tooling introduces its
own gotchas or CSS/template tricks to meet these requirements, record those *in that
project's own copy of this file* (or a linked implementation notes file) — this document
should stay focused on what the rule actually requires and why, so it's reusable across
different tech stacks.

Always re-check current rule text at eCFR.gov before relying on any of this — the CFR is
amended, and this file reflects the rules as understood at the time it was written, not a
live mirror.

## 47 C.F.R. § 1.49 — Specifications as to paper, printing, etc.

- **Paper and printed area, § 1.49(a):** Paper must be 8.5 x 11 inches. Printed material
  must fit within an area no larger than 6.5 x 9.5 inches — i.e., roughly 1-inch margins on
  a letter page, with a little more allowed depending on orientation. This applies to every
  page, including any page rotated to landscape for a wide table: the rotated page's
  printed area must still fit the same 6.5 x 9.5in envelope. Page numbers count as printed
  material and must also fall inside that area — a page number in the margin, centered
  low enough, can push the total printed height over the limit.
- **Type size, § 1.49(a):** Any typeface of at least 12-point, for *all* printed material —
  this includes footnote text and superscript footnote reference numerals, not just body
  text. (Many real-world filings use smaller footnote type as a matter of house style; the
  rule's plain text does not carve out an exception for footnotes, so treat 12-point as the
  floor everywhere unless a project's counsel says otherwise.)
- **Line spacing, § 1.49(a):** Double-spaced, with a minimum distance of 7/32 inch between
  lines. Footnotes and long indented quotations may be single-spaced, but still at minimum
  12-point type with at least 1/16 inch between lines.
- **Table of contents and summary, § 1.49(b)–(c):** Required for filings over ten pages. For
  filings over 25 pages, the summary should "seldom exceed two and never five" pages. A
  short filing (under ten pages) does not need either.
- **Electronic length equivalence, § 1.49(f)(4):** Establishes how to measure "page" length
  for filings subject to a page limit (formatted per § 1.49(a), or roughly 250 words per
  page). A Petition for Rulemaking under § 1.401 has no page limit, so this doesn't
  constrain that filing type — but it may matter for other filing types (e.g., comments in
  a docket with an explicit page limit set by the presiding order).
- **Not applicable to most rulemaking-related filings:** the rule's stapling/binding
  provisions apply to paper filings only (most practice today is electronic via ECFS), and
  § 1.49(e)'s Universal Licensing System (ULS) filing requirement applies to licensing
  matters, not rulemaking petitions, comments, or reconsideration petitions.

## Content requirements by filing type

Different filing types have different required content under Part 1, Subpart C (and, for
matters involving a specific proceeding, the presiding order or public notice governing
that docket). Confirm the applicable rule before drafting:

- **Petition for Rulemaking — § 1.401.** Must set forth the text or substance of the
  proposed rule, amendment, or rule to be repealed, together with the facts, views,
  arguments, and data supporting the request, and must indicate how the petitioner's
  interests are affected. Petitions that are moot, premature, repetitive, or frivolous may
  be dismissed without prejudice — which is itself a reason to research prior attempts
  thoroughly (see `AGENTS.md`'s ECFS research workflow) so the filing doesn't read as
  repetitive of something already denied on the merits.
- **Petition for Reconsideration — § 1.106 / § 1.429.** Must be filed within 30 days of
  public notice of the Commission action being reconsidered (§ 1.106(f) for rulemaking
  proceedings). After that window closes, reconsideration is no longer available, and a
  fresh Petition for Rulemaking under § 1.401 may be the only remaining procedural vehicle
  to raise the same substantive point — note this distinction explicitly in the filing if
  it's relevant to the procedural posture.
- **Comments / Reply Comments in an open docket.** Content requirements come from the
  Notice of Proposed Rulemaking or public notice governing that specific docket, not from a
  general Part 1 rule — read the actual Notice for filing deadlines, page limits, and any
  required certifications before drafting.
- **Request for Waiver.** Governed by § 1.3 generally (and any rule-specific waiver
  standard); must show good cause for departing from the rule as written.

## Style conventions for a legal filing (not legally required, but standard practice)

- **Caption:** centered, "Before the / FEDERAL COMMUNICATIONS COMMISSION / Washington, DC
  20554," followed by an "In the Matter of" block naming the subject and the docket/RM
  number if one has been assigned.
- **Numbered paragraphs**, not bullet points, for the substantive body — this is standard
  legal-filing convention and makes pinpoint citation to the filing itself possible later
  (e.g., "Petition ¶ 13").
- **Section headings in Roman numerals** (I., II., III. ...), **lettered subheadings**
  (A., B., C. ...) within a section, consistent with standard legal document structure.
- **Signature block and verification** (a statement, under penalty of perjury or similar,
  that the facts stated are true) at the end, per any applicable certification rule for the
  filing type.
- **No decorative color or shading** — black text and rules only, matching the plain,
  formal register of a document meant to be read and cited by agency staff and potentially
  courts. Underlining is conventionally reserved for legislative-drafting redlines
  (proposed insertions), not for emphasis.

## Verifying compliance

Whatever tool renders the final document, verify the *actual rendered output*, not just the
source markup:

- Measure the printed area on every page (including any rotated/landscape pages) and flag
  anything exceeding 6.5 x 9.5 inches.
- Confirm every text run — body, footnotes, superscript reference numerals, page numbers —
  is at least 12-point.
- Confirm line spacing meets the 7/32in (double-spaced body) / 1/16in (single-spaced
  footnotes) minimums.
- If the filing exceeds ten pages, confirm a table of contents is present with accurate,
  live (not hand-typed, easily-stale) page numbers if the tooling supports it.
- Confirm every hyperlink in the rendered document (not just the source markup) actually
  points to the correct, complete URL — some PDF viewers' automatic URL detection can
  silently truncate a URL at an unexpected character, producing a link that looks plausible
  but is wrong.
- Confirm numbered paragraphs and footnote numbers are sequential in the *rendered* output,
  not just the source — some Markdown-to-PDF pipelines silently restart list numbering when
  a heading or other block interrupts a numbered list.
