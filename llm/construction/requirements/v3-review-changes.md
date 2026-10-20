# eRUPT Reviews: Proposed Changes for v3

> Source: `files/reviews.tex` (two eBay reviewers, received 2026-10-20). Target: `proposal/v2-main.tex` (the reviewed version). Status: **proposed, not yet applied**.

## Summary

The reviews' criticisms come down to seven gaps. For each one, the suggested fix:

1. **Does history help at all?** This was reviewer 2's main concern. Add a testable first research question: does a coding agent do better with past commits, PRs and tickets than with just today's code, and does putting that history in a graph help? Then compare four setups: current code vs. history, each stored as plain text vs. as a graph. Also add stronger baselines: an unmodified Claude Code or Codex, current code plus dependencies plus docs, and simple keyword search over commit and PR text.
2. **Novelty.** Replace the long "gap" paragraph with a short table comparing the proposal to GRACG, SemanticForge, Prometheus, CCCE, Learning to Commit and Rao et al. Then state two or three contributions that aren't just a mix of prior work. Two candidates are finding hidden contracts between repos from changes that land together, and detecting history that is out of date.
3. **Out-of-date history.** Weighting recent changes more isn't enough. Also mark history that was later reverted or replaced, flag deprecated APIs and patterns rejected in review, and check that a retrieved pattern still exists in today's code. Report how often retrieval returns stale results.
4. **Evaluation validity.**
   - **Leakage:** for each test task, use only what existed before that task was created.
   - **New tasks:** in the last months, run the agent alongside developers on live eBay tasks and compare its output to what they ship.
   - **Generalization:** repeat the study on a public group of related open-source repos, and measure how build and query cost grow as more repos are added.
5. **Link to real productivity.** Set success thresholds in advance, each with a go/no-go point. The suggested numbers still need Ramesh's agreement:
   - at least 10 percentage points better than the best no-history baseline;
   - a review gate that is right at least 80% of the time when it flags something;
   - at least 20% lower token cost.

   Also report end-to-end task results and reviewer effort, not just retrieval scores.
6. **Data governance.** Replace the line promising to release "all tools and data". eBay data stays on eBay systems under NDA, and eBay approves anything published. Tools are released under a permissive license, and public datasets come only from the open-source replication. eBay keeps the royalty-free rights the call requires.
7. **Adoption path for eBay.** This was reviewer 1's main point. Offer the knowledge graph as a plug-in (an MCP server) for the coding agents eBay developers already use. Report cost savings, and make scaling up to eBay's full codebase an explicit goal with Ramesh.

The sections below give the detail for each change, the milestone shifts and how to verify the result. Edits go in a new `proposal/v3-main.tex` so the submitted v2 stays as it was.

## Context
Two eBay reviewers evaluated the submitted proposal, **`proposal/v2-main.tex`** ("Agentic Knowledge Graphs over Code History…"; it has the Repo/JIRA/Memory-Bank graphs, ~10 repos, spreading activation and the CCCE / Learning to Commit citations). `main.tex` is an older v1 and does not change.
They agree on the strengths: a real enterprise problem, a controlled comparison of retrieval strategies with baselines and statistics, provenance and traceability, and a credible team. Their weaknesses come down to **seven fixable gaps**. Each change below fixes one of them. We revise in a copy so the submitted version stays as it was.

| # | Reviewer concern | Where it lands |
|---|---|---|
| W1 | Unproven value of *history* and of *graphs* over history-agnostic or simpler approaches (R2, main point) | Motivation RQs, Methodology experiment |
| W2 | Limited novelty versus GRACG, SemanticForge, Prometheus, CCCE, Learning to Commit (R2) | Previous Work |
| W3 | Stale history: deprecated APIs and workarounds; time-weighting alone is not enough (R2) | Methodology substrate |
| W4 | Evaluation validity: leakage, historical PRs vs. new tasks, 10 Java repos may not generalize (R1, R2) | Methodology evaluation |
| W5 | Better retrieval may not mean better productivity; no success thresholds (R2) | Metrics for success |
| W6 | Data governance: "all tools and data released publicly" conflicts with proprietary data (R2) | Impact |
| W7 | Indirect benefit to eBay: developers use Claude Code and Codex with fixed navigation; no adoption or scaling path (R1) | Impact, Methodology, Milestones |

## Approach
1. `cp proposal/v2-main.tex proposal/v3-main.tex`. Edit only v3. The submitted v2 stays untouched for traceability.
2. Make the section edits below in v3.
3. Write the response traceability document `llm/construction/requirements/v3-review-response.md`. Use the same format as the existing `v2-review-response.md`: concern → change → location.

### Section edits in `v3-main.tex`

**Motivation and Objectives (W1, W7)**
- Add a falsifiable premise as **RQ0 / H1** before the current RQ1–3. Wording: *"Does mined development history, and does a graph representation of it, improve a coding agent's multi-repository work over history-agnostic context (current code, dependencies, APIs, docs)?"* RQ2 (comparing strategies) depends on the answer, so the proposal no longer assumes it.
- Reframe the deliverable as **a retrieval layer that plugs into the agents eBay developers already use**, not a new standalone agent (one sentence; detail goes in Methodology/Impact).

**Previous Work (W2)**
- Replace the long prose "gap" paragraph with a compact **positioning table**. Rows: GRACG [3], SemanticForge [4], Prometheus [17], CCCE [15], Learning to Commit [16], Rao et al. [18], Ours. Columns: *history-mined · multi-repo · new-feature synthesis · convention/contract validation · controlled retrieval comparison · staleness handling*.
- State **2–3 sharp scientific contributions** that do not just combine prior work:
  - controlled evidence on whether history helps and whether graphs help, split into those two separate factors;
  - **cross-repository implicit-contract mining** from co-change history (changes in different repos that land together);
  - **knowledge-validity (obsolescence) detection** for mined history (see W3).

**Methodology: substrate (W3)**
- Add a **knowledge-validity layer** beyond time-weighting:
  - `supersededBy` / `revertedBy` edges taken from reverts, follow-up fixes and refactors;
  - `@Deprecated` / API-removal signals;
  - patterns rejected in review comments;
  - a **liveness check** that a retrieved pattern still exists or compiles at HEAD;
  - code-survival analysis (did the pattern survive later commits?).
- Retrieved items carry a validity flag. A new metric reports the **stale-retrieval rate**.

**Methodology: core experiment (W1, W7)**
- Recast the comparison as a **2×2 ablation plus strategies**: content (current snapshot vs. history) × representation (flat/text vs. graph). The three strategies (graph query, RAG, spreading activation) run inside the history×graph cell.
- Add stronger baselines:
  - **(i)** an off-the-shelf coding agent (e.g., Claude Code / Codex) with its own native navigation;
  - **(ii)** a strong history-agnostic baseline: snapshot + dependency graph + docs;
  - **(iii)** simple history-aware retrieval: BM25/embedding over commit messages and PR text, `git log`/`blame` search, in the spirit of Learning to Commit.
- Delivery mechanism: expose the KG as a tool/MCP server. The *same* off-the-shelf agent then runs with and without it, so the comparison isolates the substrate and shows a direct adoption path.

**Methodology: evaluation (W4)**
- **Temporal leakage control**: for each task created at time *t*, the KG is rebuilt or filtered to artifacts before *t*. The resolving PR and anything after it are excluded. Note that private eBay code also lowers the risk that the model saw the solutions during pretraining.
- **New tasks, not just reconstructions**: in the final phase, a **prospective shadow-mode pilot** on live eBay tasks. The agent proposes, a developer does the work as usual, and we compare the two.
- **Generalization**: a **replication on a public multi-repository open-source ecosystem**, choosing a family of related projects with linked issue trackers. This also gives a releasable dataset (supports W6). Also run a **scaling curve**: KG build cost, incremental-update time and query latency as repos grow from 1 to ~10 to a larger eBay slice (R1's enterprise-scale point).

**Metrics for success (W5)**
- Add **pre-registered success thresholds**, each with a go/no-go decision. The values below are proposed and must be confirmed with Ramesh:
  - history beats the best history-agnostic baseline on scaffold correctness by ≥ 10 percentage points;
  - convention gate precision ≥ 0.8 with a false-positive rate the reviewer can tolerate;
  - ≥ 20% fewer tokens/cost per correct answer than the off-the-shelf agent.
- Add a **retrieval → outcome link**:
  - report end-to-end task outcomes, not only retrieval scores;
  - run a mediation/correlation analysis between retrieval recall and downstream correctness and review effort;
  - measure review effort in the shadow pilot as reviewer minutes and the number of revision rounds.

**Impact (W6, W7)**
- Replace the blanket "All tools and data … released publicly" with a **data-governance and IP paragraph**:
  - eBay source, history and JIRA data never leave eBay-controlled infrastructure;
  - students work under eBay NDA and access agreements;
  - only aggregate metrics and sanitized, eBay-approved examples are published, with eBay reviewing papers before submission;
  - **tools** are open-sourced under a permissive license;
  - **datasets** are released only from the OSS replication;
  - eBay keeps royalty-free license rights, as the eRUPT call requires.
- Add an **adoption path**: the MCP/tool interface works with eBay's existing agent harnesses. Cost and token savings are a reported outcome, tied to eBay needing control over its own agentic coding infrastructure (R1's wording). The eBay co-investigator's role is to help scale to enterprise size.
- **Risks**: add the concerns the reviewers raised (history may not help → the go/no-go gate turns this into a publishable negative result; stale knowledge; leakage) with their mitigations.

**Milestones**
- Rebalance:
  - M1–4: substrate + validity layer + leakage-safe benchmark;
  - **M4–5: go/no-go pilot on RQ0** (does history help?);
  - M5–9: the full ablation and strategy comparison;
  - M8–10: OSS replication + scaling curve;
  - M10–12: synthesis/gate + prospective shadow pilot.
- Keep the education/development/validation effort split, adjusted so validation gets ~40%.

### Constraints
- **No new uncited claims.** Any new reference, such as an OSS benchmark, must be verified with `research:add-paper` before it is cited. Otherwise describe the item generically.
- **Length**: there is no page limit, but v2 is 7 pages. Aim for ≤ 8 by moving the prose "gap" paragraph into the table and cutting duplicate sentences in Motivation and Why-academic.

### Derived artifacts (same practice as the v2 rounds)
Once v3 is approved, regenerate `proposal/eRUPT-proposal-v3.{md,docx}` with pandoc using `--reference-doc`, update the website under `docs/` and the citation matrix, and record the round in `llm/memory-bank/activeContext.md` and `progress.md` (memory-agent).

## Verification
- `cd proposal && latexmk -pdf v3-main.tex`: compiles cleanly with no undefined refs and 0 overfull boxes; check page count with `pdfinfo`.
- Run the `research:review-agent` quality gate: citations resolve, no placeholders (TBD threshold values flagged if Ramesh hasn't confirmed them), consistent terminology (JIRA casing, graph names).
- Check every row of the traceability table: each of W1–W7 points to a concrete location in v3.
- Run `research:citation-matrix` if any references were added.
