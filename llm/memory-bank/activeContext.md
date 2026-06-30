# Active Context

> Current focus. Changes frequently. Read this every session (with `progress.md`).

## As of 2026-06-30

### Current Phase
**Post-review revision — repositioning landed.** The proposal was repositioned
based on a prior-art review and **two PRs are now merged to `main`**
(chbrown13/ebay_erupt_2027): PR #1 (reposition) and PR #2 (DOE-ref removal +
§4A citation verification). Remaining work is mostly external (Ramesh's answers,
Chris's trim) plus the eventual `.docx` conversion.

### What's true right now
- **Title:** "Agentic Knowledge Graphs over Code History for Enterprise Software
  Automation" (determinism demoted out of the headline).
- **Framing** (validated by `llm/construction/requirements/prior-art-analysis.md`):
  lead with the *industry-validated problem*; novelty = a provenance KG mined from
  the org's *own* version-control history as the **unified substrate** for
  generation + convention-validation; determinism is a *supporting* property;
  validation gate framed as *support, not replacement*.
- **14 references**, all **§4A-verified** (see Recent decisions). Store =
  `references.json`; mirror = `citation-matrix.md`. 13 `verified:true`,
  [8] ICR `verified:false` (flagged, small venue, kept per user's call).
- Proposal compiles clean; markers [1]–[14] sequential and correct.
- Running example: ViewItem signals / signal handler (still eBay-unverified).

### Recent decisions (this session, 2026-06-25 → 06-30)
- **Repositioned the proposal** problem-led after the novelty gate returned
  **partial-overlap**. Rationale: the *mechanism* (KG + agents + codegen) is
  established 2024–25 prior art (GRACG is an architectural twin), but the
  *problem* (enterprise recurring-task velocity / org memory / AI-PR review
  governance) is validated by industry yet unoccupied at our specific synthesis.
  Determinism demoted because it is the most crowded, riskiest claim.
- **Removed DOE/PA-AKG as a reference** (was [2]) per Chris's PR #1 review — it's
  a separate proposal under submission at another venue. Work kept as *uncited*
  background in Previous Work + Quals. Renumbered 15 → 14 refs.
- **Kept all references for now** (user + Chris) — Chris will verify/trim later;
  [8] ICR is the obvious cut candidate.
- **Connected Consensus** as the literature-review tool (MCP, user scope, OAuth)
  and ran the **§4A verification pass** via the review-agent: all 14 exist with
  accurate metadata and correct citation usage — **no hallucinations, no
  misattributions** (13 clean, [8] flagged on venue only).
- **Chris will email Ramesh** for the open items (so no Gmail draft needed; a draft
  is saved in the session scratchpad as `ramesh-email.md` if useful).

### Immediate next steps
1. **Ramesh's answers** (Chris is handling the email): eBay VP/Head name, $120K
   sanity-check, and whether "signal / signal handler / ViewItem" are the real
   internal terms. He's out after **July 8** — tight window.
2. **Reference trim** — Chris's pass; drop [8] ICR unless a second
   convention-validation cite is wanted (Tufano [7] + Heander [9] already cover it).
3. **`.docx` conversion** — final artifact must use `files/eRUPT 2026_27
   Template...docx`; the LaTeX is the working draft. Main remaining build step.
4. Final proofread → submit to `erupt@ebay.com`.

### Open questions / blockers
- **eBay VP/Head name** — placeholder in the draft; needs Ramesh.
- **Terminology accuracy** — signal/ViewItem terms unverified; needs Ramesh.
- None blocking locally; the proposal is in a clean, compiling, verified state.

### Hard deadline
**September 21, 2026** — submit to `erupt@ebay.com` via Ramesh.
