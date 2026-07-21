# v2 Review Response — Design & Traceability

> Round of edits addressing the human review of `proposal/v2-main.tex` (2026-07-15).
> Run as constellize **design → implement → verify**. Design of the figure and
> evaluation plan by a system-architect agent; implementation into the `.tex`,
> markdown source, and website; verification by an independent review pass
> (all 15 items PASS bar one WEAK that targeted the wrong paragraphs).

## Decisions locked with the user (AskUserQuestion)
- **Methodology framing** → *keep build-order, sharpen prose* (substrate → experiment
  → synthesis; prose leans into the core; a lead-in paragraph + figure foreground it).
- **ViewItem example** → *bring back, minimal* (one concrete sentence in Impact +
  the figure's concrete anchor).
- **Timeline** → *core gets the most time* (M1–4 substrate / M5–9 experiment /
  M10–12 synthesis) + education ~20% / development ~45% / validation ~35% effort lens.

## Item-by-item mapping (review feedback → change)
| # | Feedback | Change |
|---|----------|--------|
| 1 | "of code" after "…before writing a line" | Motivation ¶1 |
| 2 | Split the one long RQ | Motivation ¶2 → **RQ1 / RQ2 / RQ3** |
| 3 | Say why it's not architectural / not a bandaid | Motivation "Why academic research?" |
| 4 | Previous Work §2 & §5 run-ons | CCCE sentence + "Our foundations" split into shorter sentences |
| 5 | What prior work is applied in industry | Folded into the gap (KG discovery [18], calibration [15], measurement [12,13]) |
| 6 | Expand the gap, tie to limitations overcome | Gap now names 3 recurring limitations + our counter to each |
| 7 | Add a methodology figure | `Figure~\ref{fig:method}` (TikZ; PNG for docx/site) |
| 8 | Flip/lean into the core | Methodology lead-in + figure foreground the experiment (order kept) |
| 9 | More detail on evaluation | New "How we evaluate" paragraph (task families, held-constant design, baselines) |
| 10 | Goals: time, speed, accuracy | Evaluation reports along **time / speed / accuracy** axes |
| 11 | Bring back ViewItem details | Minimal concrete sentence in Impact + figure anchor |
| 12 | Which statistics | Metrics: Friedman + post-hoc Wilcoxon (corrected), Cliff's δ, bootstrap 95% CIs, Krippendorff's α |
| 13 | Rebalance timeline + edu/dev/validation | M1–4 / M5–9 / M10–12 + effort lens ~20/45/35 |
| 14 | Dr. Brown lab name | "Code World No Blanket" |
| 15 | Jason: "candidate? Not yet" | "PhD **student**" (not candidate) |
| 16 | Confirm time/effort costs | **HUMAN** — effort lens added; actual costs still need Chris/Ramesh sanity-check |
| 17 | Education vs dev vs validation breakdown | Effort lens sentence in Milestones |
| 18 | Review v1 for lost framing | Restored ViewItem + weeks framing; caught & fixed "Issue Graph" → "JIRA Graph" naming; standardized JIRA casing |

## Consistency fixes found during the v1 review
- "Issue Graph" (stale name) → **JIRA Graph** in the deliverables (matched the rest of the doc + memory-bank).
- Standardized **JIRA** casing document-wide (was mixed Jira/JIRA).

## Artifacts kept in sync
- `proposal/v2-main.tex` (TikZ figure) — compiles clean, 7 pages, no overfull boxes.
- `proposal/eRUPT-proposal-v2.md` + `proposal/eRUPT-proposal-v2.docx` (regenerated via pandoc `--reference-doc`; figure embedded as `fig-method.png`).
- `docs/index.html` + `docs/proposal-v2.pdf` + `docs/fig-method.png` (website).
- Citations unchanged: 22 refs, [1]–[22], no gaps.

## Round 2 — full Zoom notes (2026-07-16)

Cross-checked the complete meeting transcript against the draft. Attribution and
three refinements applied:
- **Minhyuk** — RQ split, industry KG examples, methodology reorder/transition,
  add figure, statistics: all already in. ✅
- **Huayu** (evaluation) — made the **human baseline** explicit: correctness scored
  against the developers' own withheld PR set; time measured against **today's human
  review cost**; convention gate = the code-review validation. ✏️ refined.
- **Metrics order** — reordered "Metrics for success" to lead with the
  retrieval-strategy comparison (matches where the effort goes), then the applied
  review-cycle outcome. ✏️ refined.
- **Ramesh's ViewItem example** — enriched the minimal Impact sentence with the
  concrete features from the notes: a "selling fast" indicator / price-drop badge
  requiring 5+ services wired together. ✏️ refined.
- **Lab name** — notes flagged a wrong name ("Software Engineering and Digital
  Society Lab") to *confirm*; applied the user's correction **"Code World No
  Blanket"** — still worth a final human confirm.
- **Qualifier vs. preliminary status** — notes discussed the distinction; kept the
  safe generic **"PhD student"** (open to a specific term if desired).

## Still human-side (not tooling)
- Confirm actual time/effort **costs** of the activities and the $120K (Chris/Ramesh).
- Word proofread of the regenerated `.docx`.
- Reference trim ([8] ICR the cut candidate).
