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

> Canonical store: `references.json`. **§4A verification pass run 2026-06-30**
> (review-agent via Consensus): all 14 exist with accurate metadata and correct
> citation usage — no hallucinations, no misattributions. `[x]` = all three checks
> pass; `[~]` = checks pass but flagged for team decision. **DOE/PA-AKG removed
> per PR #1 review** (separate proposal under submission elsewhere; kept as uncited
> background). Not-yet-cited candidates are listed in `references.json`.

## Status

- **Total citations (in draft)**: 14
- **Verified (all 3 §4A checks pass)**: 14
- **Cleared to ship (`[x]`)**: 13
- **Flagged for team decision (`[~]`)**: 1 — [8] ICR (small venue)
- **Last updated**: 2026-06-30
