# eRUPT Reviews: Analysis & Recommendations for v3

> Inputs: `files/reviews.md` (two eBay reviewers, received 2026-10-20; also published as `docs/erupt-2027-reviews.md`),
> `proposal/v2-main.tex` (incl. Chris's 2026-10-20 Overleaf edits), and Chris's plan `llm/construction/requirements/v3-review-changes.md`.
> Status: **analysis only — nothing in the proposal has been changed.** Prepared 2026-10-21.

## Bottom line

Both reviewers agree on the strengths: a real enterprise problem, a controlled retrieval comparison with baselines and statistics, provenance/traceability, and a credible team. **Reviewer 1** is broadly supportive and asks for one thing: a concrete path by which eBay benefits (plug into the coding agents eBay developers already use, and scale to enterprise size). **Reviewer 2** is the harder read, with six substantive weaknesses, of which one matters most: *we assume history and graphs help rather than testing it.*

Chris's `v3-review-changes.md` diagnoses all seven gaps correctly, and I agree with almost every individual fix. My main concern is **scope**: taken together, the plan adds roughly eight new workstreams to a 12-month, one-student, $120K project. A reviewer who already doubts the core hypothesis will read a fully loaded plan as *less* credible. I recommend keeping every fix but **tiering** them (Must / Should / Could), so v3 answers every concern while committing only to what one year can deliver.

## How each reviewer reads

**Reviewer 1 (supportive, adoption-focused).** Sees the literature awareness and realism as reasons to expect progress. Weakness: unclear whether results scale beyond the evaluation setting. Reason to fund is conditional: benefit to eBay is *indirect* unless (a) the approach is integrated into the harnesses eBay developers use (they use off-the-shelf Claude Code / Codex with fixed navigation) and (b) scaling to enterprise-size codebases and comparing against existing alternatives is an explicit goal. R1 also hands us the framing: eBay needs to take control of its agentic coding infrastructure, for cost and for performance on non-typical codebases. Risks are judged no worse than any academic work in this space.

**Reviewer 2 (critical, structured).** Credits the controlled design, baselines, metrics and team. Raises six weaknesses: (1) incremental value of history and of graphs is unproven; (2) novelty vs. GRACG, SemanticForge, Prometheus, CCCE, Learning to Commit; (3) historical knowledge can be stale or wrong, and time-weighting does not fix it; (4) evaluation validity: reconstructed PRs ≠ new tasks, temporal leakage, 10 Java repos may not generalize; (5) retrieval gains may not translate to productivity, and there are no success thresholds; (6) data governance: the promise to release "all tools and data" conflicts with proprietary eBay artifacts.

## Concern → response assessment

| # | Concern (who) | Severity | Chris's v3 fix | My assessment |
|---|---|---|---|---|
| W1 | Value of history and graphs unproven (R2, main point) | **High** | RQ0/H1; 2×2 ablation (snapshot vs. history × text vs. graph); 3 strategies in the history×graph cell; 3 new baselines | **Agree — the most important change.** Go further: make the decomposition *the headline contribution* (does history help? does structure help? which retrieval?), so a negative answer is still a publishable result. Baseline (ii) "snapshot + dependency graph + docs" largely *is* the snapshot×graph cell — merge them to save a condition. |
| W2 | Limited novelty (R2) | Medium | Positioning table vs. 6 neighbors; 2–3 sharp contributions (controlled evidence; cross-repo implicit-contract mining from co-change; obsolescence detection) | Agree on the table; it also shortens the paper. **Caution:** co-change / logical-coupling mining has a long MSR history (e.g., Gall et al.'s logical coupling; Zimmermann et al., "Mining Version Histories to Guide Software Changes"). If we claim it, we must cite that line and frame ours as cross-repository and agent-facing — otherwise R2 will say this contribution isn't novel either. Lead with the controlled decomposition; list contract mining and validity detection as secondary. (Any new citation must be verified before use.) |
| W3 | Stale / wrong history (R2) | Medium | Knowledge-validity layer: supersededBy/revertedBy edges, @Deprecated signals, review-rejected patterns, liveness at HEAD, survival analysis; stale-retrieval-rate metric | Right direction, but five signals is a project in itself. **Commit to the two cheapest, highest-yield signals** — revert/supersede edges and a liveness check at HEAD — plus the stale-retrieval-rate metric. Name deprecation and review-rejection signals as extensions. |
| W4 | Evaluation validity: leakage, new tasks, generalization (R1, R2) | **High** | Temporal cutoff per task; prospective shadow-mode pilot on live eBay tasks; OSS multi-repo replication; scaling curve 1 → ~10 → larger eBay slice | Temporal cutoff is a **must** and cheap — it should have been in v2. Shadow pilot and OSS replication are *both* expensive; **choose one as committed and one as conditional.** I lean OSS replication as committed: it doesn't depend on eBay developer time, it answers generalization, and it produces the only releasable dataset (helps W6). Make the shadow pilot conditional on Ramesh securing developer participation. Scaling curve: commit to 1 → ~10 repos; the "larger eBay slice" is conditional on eBay infrastructure. |
| W5 | Retrieval ≠ productivity; no thresholds (R2) | Medium | Pre-registered go/no-go thresholds (≥10 pp over best no-history baseline; gate precision ≥ 0.8; ≥20% fewer tokens than off-the-shelf agent); end-to-end outcomes; retrieval → outcome mediation analysis | Agree on pre-registered decision gates and end-to-end outcomes. **Watch the token threshold:** injecting KG context can *raise* tokens per query; "≥20% fewer tokens than the off-the-shelf agent" could fail even when the approach works. Keep it per *correct* answer, and consider "no worse than" as the bar, with savings as a reported outcome. All numbers need Ramesh's sign-off before they go in. |
| W6 | Data governance vs. "release all tools and data" (R2) | **High (easy)** | Replace with governance/IP paragraph: data stays on eBay infra under NDA; eBay approves publications; tools open-sourced permissively; datasets only from OSS replication; eBay keeps royalty-free rights | **Agree fully — best value per word in the whole revision.** The criticized sentence ("Open Source Output: All tools and data…") came in with the Oct 20 Overleaf edits; replace it outright. |
| W7 | Indirect benefit; no adoption/scaling path (R1, main point) | **High** | Expose the KG as an MCP server for eBay's existing agents; report cost savings; enterprise scaling as explicit goal with Ramesh | **Agree strongly — the single best change.** It answers R1 directly *and* makes the experiment cleaner: the same off-the-shelf agent runs with and without the MCP server, so the comparison isolates the substrate. Make this the architectural framing of v3 (and update Fig. 1 to show the MCP boundary). |

## Scope and schedule

Counted against v2, the full plan adds: the 2×2 ablation, three extra baselines, a five-signal validity layer, temporal-leakage rebuilds, an OSS replication, a scaling curve, a prospective shadow pilot, implicit-contract mining, an MCP server, and a mediation analysis — with budget unchanged at $120K and one GRA. Proposed tiering:

- **Must** (answers the High concerns): RQ0 + 2×2 ablation; off-the-shelf-agent and simple-history-retrieval baselines; temporal leakage control; MCP delivery; governance paragraph; pre-registered decision gates; end-to-end outcome reporting.
- **Should**: positioning table; two validity signals + stale-retrieval rate; **one** of OSS replication / shadow pilot; scaling curve to ~10 repos.
- **Could** (state as extensions, or tie to "tiered funding" already mentioned in v2): implicit-contract mining as a full contribution; the full validity layer; the second of replication / pilot; enterprise-scale slice.

Suggested milestones (adjusting Chris's): **M1–4** substrate + MCP server + leakage-safe benchmark → **M4–5** go/no-go on RQ0 → **M5–9** ablation + strategy comparison → **M9–11** OSS replication (or shadow pilot) + scaling curve → **M11–12** cross-repo synthesis/gate + write-up. Chris's plan currently crams synthesis, the gate *and* the shadow pilot into M10–12.

Length: v2 is 7 pages. The positioning table replacing the prose gap and trimming "Why academic research?" should keep v3 at ~8.

## Housekeeping found while reading the repo

- **Website and derived files are behind the source.** `docs/index.html`, `docs/proposal-v2.pdf`, `proposal/v2-main.pdf` and `eRUPT-proposal-v2.{md,docx}` predate Chris's Oct 20 Overleaf edits to `v2-main.tex` (RQ wording, "Open Source Output", "Industry Outreach", risk wording). The website therefore doesn't show the paragraph Reviewer 2 criticized. The download button also says "5 pp"; the PDF is 7.
- `v3-review-changes.md` cites `files/reviews.tex`, which has since been replaced by `files/reviews.md`.
- Memory-bank (`activeContext.md`, `progress.md`) was last updated 2026-07-21; `CLAUDE.md` deadlines are from the summer.
- These reviews are now public (repo and Pages site are public). Worth a quick confirmation with Chris/Ramesh that eBay is fine with that.

## Decisions needed before editing

1. **What is v3 for?** A response before the early-November decision, a revised submission, or the kickoff plan if funded? This sets tone, length, and how much new scope to promise.
2. **Shadow pilot vs. OSS replication** — which is committed, which conditional?
3. **Success thresholds** — confirm numbers (or the "no worse than" framing for tokens) with Ramesh.
4. **Approve the Must / Should / Could tiering** (or keep Chris's full plan).
5. Whether to **link these pages from the proposal homepage** and **re-sync the website** with the Oct 20 Overleaf edits.
