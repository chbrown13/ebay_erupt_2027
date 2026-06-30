# System Patterns

> Two things live here: (A) the **proposed research system's** architecture, and
> (B) the **documentation/writing workflow** for producing this proposal.
> Living technical truth. Read after `productContext.md`.

## A. Proposed System Architecture (what the grant would build)

Two complementary approaches (deliberately redundant to mitigate risk):

### Approach 1 — Code KG Construction & Pattern Mining
- Parse eBay's Java codebase via **ASTs** to extract API usage, dependency
  relationships, and structural conventions.
- Augment with historical data: git history, PR descriptions, code-review threads.
- **Frequent sub-graphs** across the codebase form the pattern library.
  Example pattern: the ViewItem signal handler as nodes
  (`ApiGateway`, `SignalHandler`, `MetricsClient`) + typed edges
  (`imports`, `implements`, `dependsOn`).

### Approach 2 — Agentic Orchestration (three role-specific agents)
- **Ranking agents** — score candidate KG patterns by relevance to the task,
  filtering noise.
- **Generation agents** — produce code conditioned on the ranked patterns, using
  the KG as structured context instead of LLM priors alone.
- **Validation agents** — check generated PRs against KG-encoded patterns; flag
  convention deviations and breaking dependency changes.

Together → deterministic (same KG state, same output) and auditable (traceable to
historical patterns).

### Relationship to existing infrastructure
- **Compass** (eBay's enterprise KG): connects Jira → repos → commits → PRs →
  deployments → microservices. Our KG *extends* it with code-level pattern
  knowledge tickets don't capture.
- **PA-AKG / DOE Genesis** (VT): provenance-aware agentic KG for scientific
  software; its architecture (AST extraction, ranking/validation agents,
  provenance tracking) transfers directly to eBay's Java context.

## B. Documentation / Writing Workflow (how this proposal is produced)

- **Memory-Bank** (`llm/memory-bank/`): living documentation, updated each session.
- **Construction** (`llm/construction/`): design-first workspace —
  `requirements/cfp-analysis.md`, `requirements/submission-checklist.md`,
  `requirements/citation-matrix.md`, `design/proposal-design.md`,
  `sprints/proposal-writing.md`.
- **Proposal artifact**: `proposal/main.tex` (single-file LaTeX, eBay-branded).
- **Agents** (`.claude/agents/`): `proposal-agent`, `latex-agent`, `review-agent`,
  plus paper/position/memory agents.

### Writing patterns
- Design/requirements captured in `llm/construction/` before drafting.
- Citation matrix maintained alongside writing.
- Compile-check after significant LaTeX changes.

### Review patterns
- Self-review → review-agent (citations, compilation, content) → iterate.
- Human review: Jason, then Ramesh at eBay.

## Constellize tooling (installed 2026-06-25)
This repo uses the **constellize** plugin suite (memory, design, grow, craft,
deliver, harness) for structured knowledge + design workflows. The memory-bank
files here are the constellize "memory bank." Entry point for orchestrated work:
`constellize-harness:orchestrate` (assess → plan → execute).
