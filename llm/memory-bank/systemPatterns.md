# System Patterns

> Two things live here: (A) the **proposed research system's** architecture, and
> (B) the **documentation/writing workflow** for producing this proposal.
> Living technical truth. Read after `productContext.md`.

## A. Proposed System Architecture (what the grant would build)

### v2 architecture (current — `proposal/v2-main.tex`, 2026-07-07)
Scaled to the **whole multi-repository codebase** (codebase = one repository; an
eBay feature spans 5+). Three parts:

1. **A family of history-mined graphs** — not one monolithic KG but **Repo Graph**
   (services/repos, dependencies, ownership, call edges), **JIRA Graph** (work
   items → commits/PRs → external resources), and **Memory-Bank Graph** (per-repo
   living docs an agent traverses). Shared entities across graphs; the agent
   projects the task-relevant view. History edges are **time-weighted (decay)**;
   memory-bank nodes are **multi-resolution** (summary → full).
2. **The core experiment (headline contribution)** — holding the substrate fixed,
   compare **3 retrieval strategies**: (a) graph query, (b) similarity/RAG,
   (c) **spreading activation**. Report which makes an agent most efficient at
   multi-repo understanding. Backend (Neo4j/Gremlin/Auto Graph) = implementation
   footnote; topology = justified-by-scale, not novelty.
3. **Cross-repo synthesis + convention validation** — on the best retrieval
   strategy, synthesize a feature spanning several repos from mined patterns, and
   validate the resulting PRs against KG-encoded **cross-repo** conventions
   (support, not replacement). Metric: review-cycle reduction (primary),
   cross-repo scaffold accuracy (secondary).

Concepts borrowed (adopt-and-cite, not claimed): temporal decay, multi-resolution
memory, spreading activation — grounded in real literature (Collins & Loftus 1975;
Zep; H-MEM; Pavlović 2025), *not* Constellation Engine (unpublished). See
`v2-specification.md` and `v2-prior-art-analysis.md`.

### v1 architecture (superseded by v2 — kept for context)
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
- **Validation gate** — checks generated PRs against KG-encoded *historical*
  conventions; flags deviations and breaking dependency changes, **supporting
  reviewers, not replacing them** (preserves knowledge transfer).

The single substrate is the point: the same provenance-tagged history that
conditions generation also defines what conformance means at review time. Outputs
are auditable and reproducible from a fixed KG state (**determinism = a supporting
property, not the headline** — reframed 2026-06-30, see `prior-art-analysis.md`).

### Relationship to existing infrastructure
- **Compass** (eBay's enterprise KG): connects Jira → repos → commits → PRs →
  deployments → microservices. Our KG *extends* it with code-level pattern
  knowledge tickets don't capture.
- **Provenance-aware agentic-KG prior work** (team's own): architecture (AST
  extraction, ranking/validation agents, provenance tracking) transfers to eBay's
  Java context. **Used as uncited background only** — the DOE Genesis proposal it
  comes from is under submission at another venue and is **not** cited (PR #1).

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

## C. Research & Verification Workflow (established 2026-06-30)

A reusable process for grounding research-claim novelty and citations — used to
reposition this proposal and worth repeating for any new claim:

1. **Spec the deliverable first** (constellize design flow) →
   `references-spec.md` defines coverage, an impact-ranking rubric (§1A), a
   verification protocol (§4A: exists / no-hallucination / correct-citation), and
   a prior-art/novelty gate (§4C).
2. **Novelty gate FIRST** — fan-out prior-art search (Consensus) across facets +
   adversarial synthesis → `prior-art-analysis.md` with a verdict
   (novel / partial-overlap / already-solved). A bad verdict halts/repositions
   everything downstream. *Our verdict was partial-overlap → problem-led reframe.*
2a. **Problem-vs-mechanism distinction matters:** compare prior work by the
   *problem it solves*, not just architecture. Mechanism can be crowded while the
   problem is open (or vice-versa).
3. **Source references** via Consensus (real papers only; no fabricated metadata).
4. **§4A verification** via the project **`review-agent`** (`verify-citations`):
   each ref's three checks recorded in `references.json`; ship only on all-pass.
5. **Canonical store** `references.json` is the source of truth; `main.tex` and
   `citation-matrix.md` are derived views kept in sync. Renumber on add/remove.

## Constellize tooling (installed 2026-06-25)
This repo uses the **constellize** plugin suite (memory, design, grow, craft,
deliver, harness) for structured knowledge + design workflows. The memory-bank
files here are the constellize "memory bank." Entry point for orchestrated work:
`constellize-harness:orchestrate` (assess → plan → execute).
