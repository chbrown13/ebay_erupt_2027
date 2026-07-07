# Citation Matrix

Human-readable mirror of the canonical store
`references.json`. The store is the source of truth (see `references-spec.md`);
keep this table in sync with it. "Verified" = all three §4A checks pass.

## Citations

| # | Key | Authors | Title | Year | Venue | Verified | Role |
|---|-----|---------|-------|------|-------|----------|------|
| 1 | fose2026 | J. Cusati, C. Brown | A Case for Structured Knowledge Accumulation in SE Research | 2026 | ICSE-FOSE | [x] | our foundation |
| 2 | versicode | T. Wu et al. | VersiCode: Towards Version-controllable Code Generation | 2024 | arXiv:2406.07411 | [x] | version-aware code knowledge |
| 3 | gracg | K. Fedorov et al. | GRACG: Graph Retrieval Augmented Code Generation | 2025 | IEEE/ACM ASEW | [x] | mechanism (cede) — twin |
| 4 | semanticforge | W. Zhang et al. | SemanticForge: Repo-Level Code Generation via Semantic KGs + Constraints | 2025 | arXiv | [x] | mechanism + determinism contrast |
| 5 | athale | M. Athale, V. Vaddina | Knowledge Graph Based Repository-Level Code Generation | 2025 | LLM4Code | [x] | mechanism (cede) |
| 6 | autocoderover | Y. Zhang et al. | AutoCodeRover: Autonomous Program Improvement | 2024 | ACM ISSTA | [x] | mechanism (cede) — SWE-agent |
| 7 | tufano2022 | R. Tufano et al. | Using Pre-Trained Models to Boost Code Review Automation | 2022 | ICSE | [x] | review automation |
| 8 | icr2025 | T.M.N. Nimraka et al. | An Agentic-AI Solution for Intelligent Code Review | 2025 | SLAAI-ICAI | [~] | §4A checks pass; FLAGGED small venue — team to confirm |
| 9 | heander2025 | L. Heander et al. | Support, Not Automation: Towards AI-supported Code Review | 2025 | ACM FSE | [x] | support-not-replacement framing |
| 10 | janke2022 | M. Janke, P. Mäder | Graph Based Mining of Code Change Patterns From VCS Commits | 2022 | IEEE TSE | [x] | substrate premise |
| 11 | pycraft2024 | M. Dilhara et al. | Unprecedented Code Change Automation: LLMs + Transformation by Example | 2024 | ACM FSE | [x] | substrate premise |
| 12 | aku2026 | G. Bakal | Knowledge Activation: AI Skills as Institutional Knowledge Primitive | 2026 | arXiv:2603.14805 | [x] | closest on problem |
| 13 | deputydev2025 | A. Kumar et al. | Intuition to Evidence: Measuring AI's True Impact on Developer Productivity | 2025 | arXiv | [x] | problem/value evidence |
| 14 | cct5 | B. Lin et al. | CCT5: A Code-Change-Oriented Pre-trained Model | 2023 | ACM ESEC/FSE | [x] | 70% cost stat |

## v2 staged (marker TBD at draft)

Added 2026-07-07 (review-agent §4A via Consensus). These entries carry `marker: null`
and `v2: true` in `references.json` — markers will be assigned at v2 draft/renumber time.
Listed separately so the CI citation counter still parses the v1 table above unchanged.

| # | Key | Authors | Title | Year | Venue | Verified | Role |
|---|-----|---------|-------|------|-------|----------|------|
| v2 | ccce2026 | S. K. K. Parimi | CCCE: A Continuous Code Calibration Engine ... via KG Traversal and Adaptive Decision Gating | 2026 | arXiv | [x] | must-distinguish — cross-repo KG-traversal + gating, maintenance not synthesis |
| v2 | learn2commit2026 | M. Li et al. | Learning to Commit: Generating Organic Pull Requests via Online Repository Memory | 2026 | arXiv | [x] | must-distinguish — restates snapshot-vs-history thesis; single-repo |
| v2 | prometheus2025 | Z. Chen et al. | Prometheus: Unified Knowledge Graphs for Issue Resolution in Multilingual Codebases | 2025 | arXiv | [x] | mechanism cede — memory-centric coding agent over unified code KG |
| v2 | enterpriseKG2025 | N. Rao et al. | Scalable and Explainable Enterprise Knowledge Discovery Using Graph-Centric Hybrid Retrieval | 2025 | arXiv | [x] | closest enterprise multi-source substrate (Jira+Git+PRs); retrieval not generation |
| v2 | codifiedcontext2026 | A. Vasilopoulos | Codified Context: Infrastructure for AI Agents in a Complex Codebase | 2026 | arXiv | [x] | cede — memory-bank-directory idea (hot/cold memory + spec docs) |
| v2 | yates2025onboarding | R. Yates | Onboarding in Software Engineering | 2025 | Unknown Journal (likely dissertation) | [x] | impact anchor — Temporal + Rationale views ("what changed and why") |
| v2 | spreadact2025 | J. Pavlović et al. | Leveraging Spreading Activation for Improved Document Retrieval in KG-Based RAG Systems | 2025 | arXiv | [x] | adopt-cite (FR-020) — modern spreading-activation retrieval; compared retrieval mode |
| v2 | collinsloftus1975 | A. M. Collins, E. F. Loftus | A Spreading-Activation Theory of Semantic Processing | 1975 | Psychological Review | [x] | adopt-cite (FR-020) — classical origin of spreading activation |

> All 8 v2 entries pass all three §4A checks (`verified:true`). Notes: `yates2025onboarding`
> venue is "Unknown Journal" per Consensus (grounded-theory study, likely a PhD dissertation;
> its 2019 predecessor is in Empirical Software Engineering). `ccce2026` and `learn2commit2026`
> are very recent arXiv preprints with 0 citations (recency, not a venue-quality flag) — monitor.
> **Conditional (NOT staged, held in `candidatesNotYetCited`):** Zep (Rasmussen et al. 2025) and
> H-MEM (Sun et al. 2025) — add only if the v2 draft keeps decay (FR-018) / multi-resolution
> (FR-019) as named arms.

> Canonical store: `references.json`. **§4A verification pass run 2026-06-30**
> (review-agent via Consensus): all 14 exist with accurate metadata and correct
> citation usage — no hallucinations, no misattributions. `[x]` = all three checks
> pass; `[~]` = checks pass but flagged for team decision. **DOE/PA-AKG removed
> per PR #1 review** (separate proposal under submission elsewhere; kept as uncited
> background). Not-yet-cited candidates are listed in `references.json`.

## Status

- **v1 citations (numbered, in draft)**: 14
- **v2 staged (marker TBD)**: 8 — all `[x]`
- **Total in store**: 22
- **Verified (all 3 §4A checks pass, `[x]`)**: 21 (13 v1 + 8 v2)
- **Flagged for team decision (`[~]`)**: 1 — [8] ICR (small venue)
- **Conditional (not staged, in candidatesNotYetCited)**: 2 — Zep, H-MEM
- **Last updated**: 2026-07-07
