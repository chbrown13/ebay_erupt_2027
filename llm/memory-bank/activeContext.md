# Active Context

> Current focus. Changes frequently. Read this every session (with `progress.md`).

## As of 2026-06-25

### Current Phase
**Drafting / Revision.** A complete first draft of the proposal exists at
`proposal/main.tex` covering all 7 eRUPT sections. Memory bank was just
re-established to reflect actual state (it had been stale at "initialization").

### What's true right now
- Proposal title: **"Agentic Knowledge Graphs for Deterministic Code Generation."**
- All 7 CFP sections drafted: Objectives, Previous Work, Methodologies, Impact,
  Output/Milestones, Qualifications, References.
- 12-month milestone plan present (PoC M1–7, Validation M8–10, Eval M11–12).
- Running example throughout: ViewItem signals / signal handler.

### Recent decisions
- **Decision:** Re-establish (repopulate) the memory bank instead of creating new
  files. **Rationale:** all 6 core files existed but were stale stubs carrying an
  obsolete scientific-software/HPC framing from before the eBay pivot.
  **Date:** 2026-06-25.
- **Decision:** Installed the constellize plugin suite (memory/design/grow/craft/
  deliver/harness) at user request. **Date:** 2026-06-25.

### Immediate next steps (the user's stated agenda)
1. ✅ Install latest constellize plugins.
2. ✅ Refresh the stale memory bank (this pass).
3. ✅ Filled proposal Engagement fields — **Grant Amount = $120,000** (one-year);
   **VP/Head** left as a visible `[To be confirmed with Ramesh]` placeholder.
4. ✅ Wrote the **references spec** + canonical store (constellize design flow):
   `llm/construction/requirements/references-spec.md` (incl. §4A skill-driven
   verification protocol) and `references.json` (source of truth; `citation-
   matrix.md` is the mirror). Captured the 2 existing refs (unverified) + 7
   planned roles.
5. **NEXT (gated on approval):** Write the planned references into the store
   (literature review via **Consensus**, per spec §4B), then run the §4A
   verification pass using our **`review-agent verify-citations`** (Exists /
   no-hallucination / correct-citation) before syncing into `proposal/main.tex`.
   No reference ships until all three checks pass.
   - **Verifier = our review-agent**, not a constellize skill (we own the agents).
   - **Consensus is not yet connected** as an MCP connector in this session —
     needs adding; fallback = HF `paper_search` + WebSearch until then.

### Open questions / blockers
- **Grant amount** set to $120,000 (top of eRUPT range) — confirm with Ramesh it's
  the right ask before submission.
- **eBay VP/Head name?** Still needs Ramesh; placeholder in the draft.
- **Terminology accuracy:** are "signal / signal handler / ViewItem" the exact
  internal terms? Confirm with Ramesh.
- **Internal review dates** in CLAUDE.md (Jason June 22, Ramesh July 8) are at/past
  today — confirm where those stand. Ramesh is off starting July 8.

### Hard deadline
**September 21, 2026** — submit to `erupt@ebay.com` via Ramesh.
