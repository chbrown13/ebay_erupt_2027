# Active Context

> Current focus. Changes frequently. Read this every session (with `progress.md`).

## As of 2026-07-15 — human review round incorporated

Ramesh/Chris reviewed v2 and returned ~18 feedback items; all addressed this
session (constellize design → implement → verify). Traceability:
`llm/construction/requirements/v2-review-response.md`. Highlights:
- **Motivation:** one long RQ split into **RQ1/RQ2/RQ3**; added a "not an
  architectural gap / not a bandaid" framing; "before writing a line **of code**."
- **Previous Work:** cleaned the CCCE + "Our foundations" run-ons; the **gap**
  now names what's applied in **industry** (KG discovery [18], calibration [15],
  measurement [12,13]) and the 3 limitations we overcome.
- **Methodology:** added a **TikZ figure** (`\ref{fig:method}`) foregrounding the
  core experiment; new **"How we evaluate"** paragraph (task families,
  held-constant single-variable design, 2 baselines) reporting **time / speed /
  accuracy** deltas.
- **Milestones:** timeline rebalanced so the **core experiment gets the most time**
  (M1–4 / **M5–9** / M10–12) + effort lens **~20% education / ~45% dev / ~35%
  validation**; statistics named (Friedman + post-hoc Wilcoxon corrected, Cliff's
  δ, bootstrap 95% CIs, Krippendorff's α).
- **Impact:** minimal concrete **ViewItem** example restored.
- **Qualifications:** Dr. Brown's lab = **"Code World No Blanket"**; Jason =
  **"PhD student"** (not candidate).
- **Consistency:** fixed stale "Issue Graph" → **JIRA Graph**; standardized JIRA
  casing doc-wide.
- **Artifacts re-synced:** `.tex` (7 pp, clean), regenerated `.docx` (figure
  embedded) + markdown source, website `docs/` (figure PNG + PDF). 22 refs
  unchanged. Verified by an independent review pass (all items PASS).
- **Still human-side:** confirm actual **time/effort costs** + $120K (item was a
  question to the team, not a tooling task); Word proofread; ref trim.

## As of 2026-07-07

### Current Phase
**v2 shipped and live.** The proposal was scaled up from a single ViewItem page
to the whole multi-repository codebase. **PR #8 is merged to `main`**
(chbrown13/ebay_erupt_2027) and the website is **published on GitHub Pages**.
Remaining work is external (Ramesh's answers, Chris's ref trim) plus the eventual
`.docx` conversion for submission.

### What v2 is (the scale-up)
- **Unit of analysis:** *codebase = one GitHub repository*; an eBay feature spans
  several (**5+, per Ramesh**). v1 targeted one ViewItem page in one repo.
- **Thesis unchanged:** a provenance-aware KG mined from the org's **own
  version-control history**. v2 extends it to multi-repo and mines from commits,
  **GitHub PRs, JIRA work items, code patterns, and external resources**.
- **Headline contribution (locked):** an **empirical 3-way comparison of
  history-retrieval strategies** — graph query vs. similarity/RAG vs.
  **spreading activation** — "which makes a coding agent most efficient at
  multi-repo understanding." Staked on **cross-repo feature synthesis** +
  cross-repo convention validation.
- **Substrate:** a *family* of graphs — **Repo / JIRA / Memory-Bank** — with
  time-weighted (decay) edges + multi-resolution memory-bank nodes (concepts
  borrowed from spreading-activation memory systems; reviewed Constellation
  Engine 2026-07-07, cited to real literature, not the product).
- **Demoted:** determinism (dropped as a claim) and graph-of-graphs (ceded as
  known prior art — justified by scale, not sold as novel).
- **Metric (locked):** primary = review-cycle/comment reduction; secondary =
  cross-repo feature-scaffold accuracy. Case-study bound = **~10 related repos**.

### What's true right now
- **Two proposals side-by-side:** `proposal/main.tex` (v1, untouched — also
  recently edited via **Overleaf**, see below) and `proposal/v2-main.tex` (v2).
  v2 compiles clean (0 errors, 5 pages; extra page = the 22-ref list).
- **References: 22 total** (14 v1 + 8 v2), all **§4A-verified** except [8] ICR
  (`[~]` flagged, small venue, kept). Store = `references.json`; mirror =
  `citation-matrix.md`. 8 v2 additions verified 2026-07-07.
- **Novelty gate (v2):** verdict `partial-overlap` →
  `v2-prior-art-analysis.md`. Two sharpest neighbors pre-empted in the draft:
  **CCCE** (cross-repo KG but *maintenance*, not synthesis) and **Learning to
  Commit** (our snapshot-vs-history thesis but *single-repo*).
- **Verification:** review-agent confirmed all **7 acceptance criteria MET**,
  citations clean; CI *Paper Quality Gate* **green + APPROVED** on PR #8.
- **Website LIVE:** https://chbrown13.github.io/ebay_erupt_2027/ (source =
  `main` `/docs`; Chris enabled Pages). Also a Claude artifact preview exists.

### Spec / provenance
- v2 spec: `llm/construction/requirements/v2-specification.md` (FR/NFR/ACs,
  §1.5 headline decision, §7 reference tee-up). Source notes:
  `files/preliminary-meeting-notes.md` (Jason + Chris).

### Recent decisions (this session, 2026-07-07)
- Locked the **retrieval axis** as the headline 3-way comparison (backend =
  footnote; topology = justified-by-scale architecture, not novelty).
- Borrowed 3 memory-systems concepts (decay / multi-resolution / spreading
  activation) — adopt-and-cite only; spreading activation became comparison arm
  (c). Constellation Engine itself **not cited** (unpublished single-agent
  project).
- Expanded case-study bound 3 → ~10 repos on Ramesh's "5+ repos per feature."
- Published the website as an **Artifact** first (no repo admin → couldn't enable
  Pages myself); Chris then merged PR #8 and enabled Pages.

### Immediate next steps
1. **`.docx` DONE** → `proposal/eRUPT-proposal-v2.docx` (+ regenerable
   `proposal/eRUPT-proposal-v2.md` source), built via `pandoc --reference-doc`
   against the eBay template. **Needs a human Word proofread** (formatting the
   tooling can't verify).
2. **Reference trim** (Chris) — 22 is heavy for 2–3 pages; [8] ICR obvious cut.
3. **$120K** sanity-check (Chris/Ramesh).
4. Confirm v2 supersedes v1 → final proofread → submit to `erupt@ebay.com`.

### Resolved 2026-07-07 (from Chris's Overleaf edits, reconciled into v2)
- **eBay VP/Head = Rami El-Charif** — placeholder filled. Carried into v2
  (engagement table), memory-bank, website.
- **Chris's PI bio updated** (his own wording) — carried into v2 Qualifications.
- Section renamed **"Motivation and Objectives"**; added an empirical-study
  justification sentence (reinforces v2's headline).
- **NOT carried:** Chris's expanded v1 Previous-Work paragraphs — that Overleaf
  diff is a merge artifact (duplicated paras, mismatched citation numbers from a
  ~15-ref v1); v2's own Previous Work supersedes it. Flagged for the team.

### Open questions / watch-outs
- **$120K** — Chris/Ramesh sanity-check still open (not blocking).
- **v1 (`main.tex`) is diverging** — Chris edits it via Overleaf (~15 refs, new
  motivation prose). If v2 is the submission, v1 divergence is moot; confirm.

### Hard deadline
**September 21, 2026** — submit to `erupt@ebay.com` via Ramesh.
