# Progress

> Historical record + status. Read every session with `activeContext.md`.
> Updated 2026-07-07.

## Current Phase: v2 shipped & live — headed to `.docx` + submission

## Completed
- [x] Project scaffolded from paper-template (memory-bank, construction, agents)
- [x] CFP analyzed → `llm/construction/requirements/cfp-analysis.md`
- [x] Conversations with Ramesh captured → `files/project_notes.md`
- [x] Full first draft (v1) — all 7 eRUPT sections (`proposal/main.tex`)
- [x] eBay-branded LaTeX styling; GitHub Actions (PR review)
- [x] constellize suite installed + Consensus MCP connected (2026-06-25)

## v1 track (completed)
- [x] Prior-art review → `prior-art-analysis.md` (verdict partial-overlap)
- [x] **Repositioned** problem-led; determinism demoted; support-not-replace gate
- [x] **PR #1 + #2 merged** (2026-06-30) — reposition; removed DOE ref → 14 refs
- [x] **§4A verification** — 14 refs (13 verified, [8] ICR flagged)
- [x] CI repaired (PRs #4–#7): Paper Quality Gate + Pages checks healthy

## v2 track (completed 2026-07-07)
- [x] **v2 spec** from meeting notes → `v2-specification.md` (codebase = repo;
      multi-repo; features span 5+ repos)
- [x] Reviewed **Constellation Engine**; borrowed 3 concepts (temporal decay,
      multi-resolution nodes, spreading activation) — adopt-and-cite, product
      not cited
- [x] **v2 novelty gate** (Consensus + review-agent) → `v2-prior-art-analysis.md`
      (verdict partial-overlap; CCCE + Learning to Commit as sharpest neighbors)
- [x] **Headline locked** = empirical retrieval-strategy comparison (graph-query
      vs RAG vs spreading-activation), staked on cross-repo synthesis
- [x] **8 new refs §4A-verified** → `references.json` now **22 total** (21 `[x]`,
      1 `[~]`), `citation-matrix.md` mirrored
- [x] **`proposal/v2-main.tex`** drafted (side-by-side with v1), compiles clean
- [x] **review-agent verification**: all 7 acceptance criteria MET, citations clean
- [x] **Website** built (`docs/`): standalone HTML render + PDF; Claude artifact
- [x] **PR #8 merged** to `main`; CI green + **APPROVED**
- [x] **GitHub Pages LIVE** → https://chbrown13.github.io/ebay_erupt_2027/

## v2 review round (completed 2026-07-15)
- [x] Human review (~18 items) addressed → `v2-review-response.md` (design/traceability)
- [x] RQ split (RQ1/RQ2/RQ3); not-a-bandaid framing; gap expanded w/ industry + limitations
- [x] **Methodology figure** (TikZ `\ref{fig:method}`) + "How we evaluate" (time/speed/accuracy)
- [x] Timeline rebalanced (M1–4 / M5–9 core / M10–12) + edu/dev/validation effort lens
- [x] Statistics named (Friedman/Wilcoxon/Cliff's δ/bootstrap CIs/Krippendorff's α)
- [x] Lab = "Code World No Blanket"; Jason = "PhD student"; "Issue"→"JIRA Graph"; JIRA casing
- [x] Re-synced all 3 artifacts (`.tex` 7 pp, `.docx`+md, website); verified independently

## In Progress / External
- [x] **VP/Head resolved → Rami El-Charif** (Chris's Overleaf edit, reconciled into v2)
- [x] Reconciled Chris's Overleaf edits into v2 (VP name, PI bio, heading, empirical
      justification); did NOT import the v1 Previous-Work merge artifact
- [ ] (External) Chris/Ramesh: $120K sanity-check
- [ ] (External) Chris: reference verify/trim ([8] ICR is the cut candidate)
- [ ] Confirm v1 (`main.tex`, still edited via Overleaf) is not the submission path

## Upcoming (critical path to submission)
- [x] **Convert v2 → eBay `.docx`** → `proposal/eRUPT-proposal-v2.docx` (pandoc
      `--reference-doc`; markdown source committed). Needs human Word proofread.
- [ ] Human Word proofread of the `.docx` (formatting)
- [ ] $120K sanity-check + reference trim (Chris)
- [ ] Confirm v2 supersedes v1 for submission
- [ ] Final proofread → submit to erupt@ebay.com before **Sept 21, 2026**

## Known issues / risks
- 22 refs is heavy for a 2–3 page proposal — trim expected (Chris).
- Final submission format is .docx; draft lives in LaTeX — conversion pending.
- eBay VP/Head name still a placeholder.
- Someone is editing v1 via Overleaf — watch for divergence.

## v2 Milestone timeline (from `v2-main.tex`)
| Window | Deliverable |
|--------|-------------|
| Months 1–5 | Multi-graph history substrate (Repo / JIRA / Memory-Bank) |
| Months 6–9 | Retrieval-strategy comparison (the core research result) |
| Months 10–12 | Cross-repo synthesis + validation gate + publications |
