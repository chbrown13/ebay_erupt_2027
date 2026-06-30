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
5. **NEXT (ultracode workflow, gated on approval):**
   1. **Novelty gate FIRST** (spec §4C) — prior-art search via Consensus →
      `prior-art-analysis.md` with closest work + gap statement + verdict. If
      "already solved / major overlap," STOP and escalate.
   2. **Source** the planned references via **Consensus** (connected), scoring
      each by **impact** (spec §1A) to decide Should-tier inclusion within the
      ~5–8 budget; log exclusions.
   3. **Verify** via `review-agent verify-citations` (Exists / no-hallucination /
      correct-citation) — nothing ships until all three pass.
   4. Sync `references.json` → `proposal/main.tex` (split FOSE/DOE) + matrix.
   - **Verifier = our review-agent** (we own the agents; no constellize skill).
   - **Consensus connected** (`mcp__consensus__search`, user scope). Backup = HF
     `paper_search` + WebSearch only if rate-limited.

### Decisions (2026-06-25)
- Dropped Nice cites FR-008 (RAG) and FR-009 (AI-PR review) — keep list lean.
- Compass cited honestly as eBay-internal / personal communication (no fake paper).
- Keep manual `[n]` references (no BibTeX) for ~6 entries.
- Added impact-ranking (§1A) + prior-art/novelty gate (§4C) to the spec.

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
