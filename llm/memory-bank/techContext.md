# Technical Context

> Tools, conventions, and setup. Reference as needed. Changes when tooling changes.

## This repo's toolchain (producing the proposal)

- **Document**: LaTeX — `proposal/main.tex` is a single self-contained file
  (`article` class, 11pt, letterpaper). eBay-branded colors defined inline
  (`ebay-dark #353744`, `ebay-green #00ab44`, `ebay-gray #444444`).
- **Packages**: geometry, titlesec, tabularx, booktabs, hyperref, amsmath,
  parskip, microtype, lmodern.
- **References**: 14 inline `[n]` references (no `.bib`). Canonical store =
  `llm/construction/requirements/references.json` (source of truth; `main.tex` +
  `citation-matrix.md` are derived). All **§4A-verified** 2026-06-30.
- **Version control**: Git (branch `main`).
- **CI/CD**: GitHub Actions in `.github/` — Pages deploy + PR review workflow.
- **Presentation**: separate `presentation/main.tex`.

### Build / compile
The proposal is LaTeX. Compile with `pdflatex proposal/main.tex` (run twice for
refs) or via the `latex-agent`. There is no Makefile; keep `main.tex` compiling
cleanly after edits. Final eBay submission uses the **.docx template** in
`files/` — the LaTeX is the working draft; plan a docx conversion before submit.

## Research & literature tooling

- **Consensus** (MCP connector, added 2026-06-30): AI search over peer-reviewed
  papers. Tool: `mcp__consensus__search`. Endpoint `https://mcp.consensus.app/mcp`
  (HTTP transport), **user scope**, OAuth (`claude mcp add --transport http
  consensus <url> -s user`; authenticate via `/mcp`; reconnect picks up logged-in
  account for full 20 results vs. top-3). **Rate limit:** ≤3 searches/batch; on
  rate-limit error wait ~30s. Primary lit-review tool; backup = Hugging Face
  `paper_search` + WebSearch/WebFetch.
- **Verification**: project `review-agent` (`.claude/agents/review-agent.md`,
  `verify-citations`) runs the §4A 3-point check using Consensus for
  existence/metadata.
- **GitHub workflow**: `gh` CLI (authed as djjay0131); origin =
  `chbrown13/ebay_erupt_2027`. Work via feature branch → PR → merge (PRs #1, #2).

## Proposed system's stack (what the grant would build — not built here)

- **Language target**: eBay enterprise **Java** codebase.
- **Extraction**: Abstract Syntax Trees (ASTs) for code structure; git/PR mining.
- **Representation**: knowledge graph (entities + typed edges); frequent-subgraph
  mining for the pattern library.
- **Agents**: LLM-based ranking / generation / validation agents.
- **Evaluation**: benchmarking study vs. baselines (vanilla LLM, RAG); metrics =
  pattern retrieval precision/recall, agent-PR acceptance rate, developer-time
  reduction. Possible developer user study.

## Key reference materials (in `files/`)

| File | What it is |
|------|-----------|
| `2027 eRUPT Academic Research Grants - External (1).pdf` | The CFP |
| `eRUPT 2026_27 Template ... .docx` | Required submission template |
| `eRupt_example.docx` | Prior funded eRUPT proposal (example) |
| `cusati-brown-fose2026-preprint.pdf` | Our FOSE 2026 position paper |
| `doe-genesis.tex`, `doe-abstract.pdf` | DOE PA-AKG sibling project |
| `amazon.pdf` | Related approach background |
| `project_notes.md` | Raw notes from Ramesh conversations (source of truth for intent) |

## Conventions
- Convert relative dates to absolute in docs (today's baseline: 2026-06-30).
- Memory-bank = single source of truth; cross-reference, don't duplicate.
- Don't overwrite reference materials in `files/`.
- `references.json` is canonical; keep `main.tex` + matrix in sync (renumber refs
  on any add/remove).

## Technical Decisions

| Decision | Rationale | Date |
|----------|-----------|------|
| Single-file LaTeX for the draft | Short proposal (~2–3 pp); simpler than multi-file | 2026-06 |
| ViewItem signals as scoped case study | Well-bounded, high-frequency pattern; de-risks KG extraction | 2026-06 |
| Extend Compass rather than replace | Leverages eBay's existing KG investment | 2026-06 |
| Installed constellize plugin suite | Structured memory/design/quality workflows | 2026-06-25 |
| Connected Consensus MCP for lit review | Peer-reviewed search to ground citations / novelty (no hallucination) | 2026-06-30 |
| **Repositioned proposal problem-led** | Novelty gate = partial-overlap; mechanism crowded, problem open | 2026-06-30 |
| **Demoted "deterministic" from headline** | Most-crowded claim; provenance-reproducibility kept as supporting | 2026-06-30 |
| **Removed DOE/PA-AKG as a citation** | Separate proposal under submission elsewhere (PR #1 review) | 2026-06-30 |
| §4A verification before shipping refs | No hallucinated/misattributed citations in submission | 2026-06-30 |
