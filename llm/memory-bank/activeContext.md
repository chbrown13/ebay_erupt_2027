# Active Context

> Current focus. Changes frequently. Read this every session (with `progress.md`).

## As of 2026-06-30

### Current Phase
**Revision after first team review.** The proposal was **repositioned** based on a
prior-art review and **merged to `main` via PR #1** (chbrown13/ebay_erupt_2027).
Now actioning review feedback and prepping the Ramesh draft.

### What's true right now
- Proposal title: **"Agentic Knowledge Graphs over Code History for Enterprise
  Software Automation"** (determinism demoted out of the headline).
- Framing (validated by prior-art review, `prior-art-analysis.md`): lead with the
  industry-validated problem; novelty = a provenance KG mined from the org's *own*
  version-control history as the **unified substrate** for generation +
  convention-validation; determinism is a supporting property; validation gate
  framed as *support, not replacement*.
- **14 references** in the draft (was 15 — DOE/PA-AKG removed, see below). Store =
  `references.json`; mirror = `citation-matrix.md`. All `verified:false`.
- Running example throughout: ViewItem signals / signal handler.
- Compiles clean; markers [1]–[14] sequential and consistent.

### PR #1 review decisions (C. Brown, 2026-06-30)
1. **Keep all references for now** — Chris will verify/trim later. ✅
2. **Removed DOE/PA-AKG as a reference** [was [2]] — it's a separate proposal under
   submission at another venue; do **not** cite. Work retained as *uncited*
   background in Previous Work + Quals. ✅ (renumbered 15→14)
3. **"Good job demoting deterministic."** ✅

### Immediate next steps
1. **§4A citation-correctness pass** — run `review-agent verify-citations` over the
   14 refs (existence/metadata already confirmed via Consensus; `citationCorrectness`
   still pending). Note: Chris said he'll also verify/trim, so coordinate.
2. **Confirm with Ramesh** (he is OUT starting July 8 — tight window):
   eBay VP/Head name, grant amount ($120K) sanity-check, and whether
   "signal / signal handler / ViewItem" are the exact internal terms.
3. **`.docx` conversion** — final artifact must use the eBay template
   (`files/eRUPT 2026_27 Template...docx`); the LaTeX is the working draft.
4. Optional: tighten any section per further team comments on PR #1.

### Open questions / blockers
- **eBay VP/Head name** — still a placeholder in the draft; needs Ramesh.
- **Terminology accuracy** — confirm signal/ViewItem terms with Ramesh.
- **Draft-to-Ramesh** target was ~July 8 (he's off after); confirm timing.

### Hard deadline
**September 21, 2026** — submit to `erupt@ebay.com` via Ramesh.
