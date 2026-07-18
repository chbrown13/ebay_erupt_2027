# Technical Context

> Tools, conventions, and setup. Reference as needed. Changes when tooling changes.
> **v2 (2026-07-07):** added the `.docx` pipeline, the website, and v2 refs.

## This repo's toolchain (producing the proposal)

- **Document (two side-by-side):** `proposal/main.tex` (v1) and
  `proposal/v2-main.tex` (v2, current). `article` class, 11pt, letterpaper,
  eBay-branded colors inline (`ebay-dark #353744`, `ebay-green #00ab44`).
  ⚠️ v1 `main.tex` is also edited by Chris via **Overleaf** — diverging; v2 is the
  submission path (assumed).
- **Packages**: geometry, titlesec, tabularx, booktabs, hyperref, amsmath,
  parskip, microtype, lmodern.
- **References**: inline `[n]` markers (no `.bib`). Canonical store =
  `llm/construction/requirements/references.json` (source of truth; `.tex` +
  `citation-matrix.md` derived). **22 total** (14 v1 + 8 v2), all §4A-verified
  except [8] ICR (flagged). Keep in sync; renumber on add/remove.
- **Version control**: Git, branch `main`. Feature-branch → PR → merge.

### Build / compile
- LaTeX: `latexmk -pdf proposal/v2-main.tex` (or `pdflatex` twice). Keep it
  compiling clean after edits. v2 = 5 pages (extra page = 22-ref list).
- **`.docx` submission artifact** (`proposal/eRUPT-proposal-v2.docx`): built from a
  **markdown source** (`proposal/eRUPT-proposal-v2.md`) via
  `pandoc eRUPT-proposal-v2.md --reference-doc="files/eRUPT 2026_27 Template...docx" -o eRUPT-proposal-v2.docx`.
  The `--reference-doc` applies the eBay template's Word styles (Heading1, Normal,
  Table). **Markdown intermediate, not LaTeX** — pandoc chokes on the custom
  macros (`\ehr`, custom `\maketitle`). Regenerate from the `.md` after any edit.
- Tools present: `pandoc`, `pdftotext`, `pdftoppm` (poppler), full TeXLive.
  **No LibreOffice/soffice.**
- **Methodology figure** (`fig:method`): authored as **TikZ**. The inline version in
  `v2-main.tex` is wrapped in `\resizebox{\textwidth}{!}{...}` so it always fits.
  Because the `.docx`/website come from **markdown, not LaTeX**, the figure is also
  compiled standalone (`scratchpad/fig-method.tex`, `standalone` class) → `pdftoppm
  -r 200` → **`fig-method.png`**, committed to both `proposal/` and `docs/` and
  referenced as an image from the `.md` and `index.html`. Regenerate the PNG whenever
  the figure changes. ⚠️ TikZ gotcha: style names `out`, `cap`, `in` collide with
  reserved keys — use `outb`/`capt` etc.

### Website
- `docs/` = GitHub Pages site: `docs/index.html` (standalone HTML render of v2) +
  `docs/proposal-v2.pdf`. Generated from the same content as the reading page.
- **Live:** https://chbrown13.github.io/ebay_erupt_2027/ (source = `main` `/docs`;
  Chris enabled Pages — needs repo **admin**, which djjay0131 lacks).
- Also a Claude **Artifact** (HTML + embedded PDF download) for no-admin publishing —
  the fastest way to share the *latest* draft without waiting on a PR merge.
  **Stable URL:** https://claude.ai/code/artifact/68669b70-ef62-425a-8b9b-8e0045335f24
  Built by a small Python step that reads `docs/index.html`, inlines `fig-method.png`
  and `v2-main.pdf` as `data:` URIs (CSP blocks external hosts), strips the outer
  `<html>/<head>/<body>` skeleton, and writes `scratchpad/proposal-v2-artifact.html`.
  **Republish the same scratchpad file path to keep the URL** (a new path mints a new URL).

## Research & literature tooling

- **Consensus** (MCP, user scope, OAuth): `mcp__consensus__search`. Primary
  lit-review + §4A-verification source. **Rate limit ≤3/batch; wait ~30s on 429.**
  Backup = Hugging Face `paper_search`, WebSearch/WebFetch.
- **Verification**: project `review-agent` runs the §4A 3-point check
  (exists / no-hallucination / correct-citation) via Consensus.
- **GitHub**: `gh` CLI (authed djjay0131, **push not admin**); origin =
  `chbrown13/ebay_erupt_2027`. PRs #1–#9. CI = `.github/workflows/pr-review.yml`
  (Paper Quality Gate: placeholder scan scoped to `paper/ proposal/`, citation
  matrix counter, LaTeX compile).

## Proposed system's stack (what the grant would build — not built here)

- **Target**: eBay enterprise **Java**, multi-repository (case-study bound ~10 repos).
- **Extraction**: ASTs + git/PR/JIRA mining across repos → a **family of graphs**.
- **Retrieval (the experiment)**: graph query vs. similarity/RAG vs. spreading
  activation; time-weighted + multi-resolution.
- **Agents**: ranking / generation / validation; cross-repo synthesis + gate.
- **Evaluation**: primary = review-cycle reduction; secondary = cross-repo
  scaffold accuracy; supporting = retrieval precision/recall, onboarding success.

## Key reference materials (in `files/`)

| File | What it is |
|------|-----------|
| `2027 eRUPT Academic Research Grants - External (1).pdf` | The CFP |
| `eRUPT 2026_27 Template ... .docx` | Required submission template (reference-doc for pandoc) |
| `eRupt_example.docx` | Prior funded eRUPT proposal (example) |
| `cusati-brown-fose2026-preprint.pdf` | Our FOSE 2026 position paper [1] |
| `preliminary-meeting-notes.md` | **v2 source** — Jason + Chris notes |
| `project_notes.md` | Raw notes from Ramesh conversations |
| `doe-genesis.tex`, `doe-abstract.pdf` | DOE PA-AKG sibling (uncited — separate venue) |
| `amazon.pdf` | Related approach background |

## Conventions
- Convert relative dates to absolute (today's baseline: **2026-07-18**).
- Memory-bank = single source of truth; cross-reference, don't duplicate.
- Don't overwrite reference materials in `files/`.
- `references.json` canonical; `.tex`/matrix/`.md`/docx are derived — keep in sync.

## Technical Decisions

| Decision | Rationale | Date |
|----------|-----------|------|
| Single-file LaTeX for the draft | Short proposal (~2–3 pp) | 2026-06 |
| Extend Compass rather than replace | Leverages eBay's existing KG investment | 2026-06 |
| Consensus MCP for lit review + §4A | Peer-reviewed grounding, no hallucination | 2026-06-30 |
| Repositioned problem-led; demoted determinism | Novelty gate = partial-overlap | 2026-06-30 |
| **v2: scale to multi-repo (codebase = repo)** | Meeting notes; a feature spans 5+ repos (Ramesh) | 2026-07-07 |
| **v2: empirical retrieval-comparison = headline** | Only open claim; sidesteps crowded mechanisms | 2026-07-07 |
| **Borrowed decay / multi-res / spreading-activation** | Adopt-and-cite (real lit); NOT Constellation Engine | 2026-07-07 |
| **v2 side-by-side (`v2-main.tex`), v1 untouched** | Team diff; v1 under Overleaf edits | 2026-07-07 |
| **`.docx` via pandoc markdown → `--reference-doc`** | Applies eBay template styles; LaTeX macros break pandoc | 2026-07-07 |
