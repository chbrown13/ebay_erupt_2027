# Architectural Decisions

Decisions are recorded in ADR (Architecture Decision Record) format.

## ADR-001: Use template-paper project structure

- **Date**: 2026-03-08
- **Status**: Accepted
- **Context**: Need a structured approach to writing academic papers with agent assistance
- **Decision**: Use memory-bank + construction + agent architecture
- **Consequences**: Clear workflow, traceable progress, consistent quality gates

## ADR-002: Scale v2 from a single page to the whole multi-repository codebase

- **Date**: 2026-07-07
- **Status**: Accepted
- **Context**: v1 scoped to one ViewItem page in one repo. Meeting notes (Jason +
  Chris) and Ramesh's input reframe the real problem: a *codebase = one
  repository*, and an eBay feature spans **5+ repositories**. Onboarding, cross-repo
  feature velocity, and the review bottleneck are the true pains.
- **Decision**: Redefine the unit of analysis as multi-repository; mine a *family*
  of history graphs (Repo / JIRA / Memory-Bank) from commits, PRs, JIRA work items,
  code patterns, and external resources. v2 lives side-by-side (`v2-main.tex`); v1
  untouched.
- **Consequences**: Bigger ambition + eBay relevance, but more crowded prior art;
  requires scope discipline (case-study bound ~10 repos) and a fresh novelty gate.

## ADR-003: Make the empirical retrieval-strategy comparison the headline contribution

- **Date**: 2026-07-07
- **Status**: Accepted
- **Context**: The v2 novelty gate (`v2-prior-art-analysis.md`) returned
  **partial-overlap** — every *mechanism* (graph-of-graphs, memory-bank traversal,
  decay/multi-resolution/spreading-activation) is crowded 2025–26 prior art.
- **Decision**: Lead with the one open thing — an empirical head-to-head of three
  retrieval strategies (graph query vs. similarity/RAG vs. spreading activation) for
  multi-repo agent understanding — staked on cross-repo feature *synthesis*. Demote
  topology to justified-by-scale, backend to a footnote; drop determinism entirely.
  Pre-empt CCCE and Learning to Commit in-text.
- **Consequences**: Sidesteps every mechanism-novelty fight; borrowed concepts are
  adopt-and-cite only (real literature, not Constellation Engine). Requires a
  concrete metric (locked: review-cycle reduction primary; cross-repo scaffold
  accuracy secondary).
