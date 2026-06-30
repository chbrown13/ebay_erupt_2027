# Technical Context

> Tools, conventions, and setup. Reference as needed. Changes when tooling changes.

## This repo's toolchain (producing the proposal)

- **Document**: LaTeX — `proposal/main.tex` is a single self-contained file
  (`article` class, 11pt, letterpaper). eBay-branded colors defined inline
  (`ebay-dark #353744`, `ebay-green #00ab44`, `ebay-gray #444444`).
- **Packages**: geometry, titlesec, tabularx, booktabs, hyperref, amsmath,
  parskip, microtype, lmodern.
- **References**: currently inline `[1]`, `[2]` style (no .bib file yet). If the
  reference list grows, consider BibTeX.
- **Version control**: Git (branch `main`).
- **CI/CD**: GitHub Actions in `.github/` — Pages deploy + PR review workflow.
- **Presentation**: separate `presentation/main.tex`.

### Build / compile
The proposal is LaTeX. Compile with `pdflatex proposal/main.tex` (run twice for
refs) or via the `latex-agent`. There is no Makefile; keep `main.tex` compiling
cleanly after edits. Final eBay submission uses the **.docx template** in
`files/` — the LaTeX is the working draft; plan a docx conversion before submit.

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
- Convert relative dates to absolute in docs (today's baseline: 2026-06-25).
- Memory-bank = single source of truth; cross-reference, don't duplicate.
- Don't overwrite reference materials in `files/`.

## Technical Decisions

| Decision | Rationale | Date |
|----------|-----------|------|
| Single-file LaTeX for the draft | Short proposal (~2–3 pp); simpler than multi-file | 2026-06 |
| ViewItem signals as scoped case study | Well-bounded, high-frequency pattern; de-risks KG extraction | 2026-06 |
| Extend Compass rather than replace | Leverages eBay's existing KG investment | 2026-06 |
| Installed constellize plugin suite | Structured memory/design/quality workflows | 2026-06-25 |
