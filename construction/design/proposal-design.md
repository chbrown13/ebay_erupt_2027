# Design: Agentic Knowledge Graphs for Deterministic Code Generation

## Objective
Design and write a 2-3 page eRUPT proposal for eBay that proposes using agentic knowledge graphs (KGs) to capture historical code patterns, team conventions, and project context — enabling AI coding agents to deterministically generate solutions for recurring development tasks at eBay.

## Target Venue Alignment
- **Venue**: eRUPT 2027 (eBay Research and University Partnership for Technology)
- **Topic Area**: AI-assisted software engineering; knowledge graphs for code generation
- **Relevance**: Addresses eBay's need to automate recurring code patterns (e.g., adding signals to ViewItem pages), reduce developer onboarding time, and create trustworthy validation pipelines for agentic PRs

## Background

### Problem Context
- eBay has a large, multi-year codebase (primarily Java) with recurring patterns (e.g., "adding signals" takes 2-4 weeks per instance)
- Agentic code generation is promising but lacks **determinism** and **historical awareness**
- Code review is the bottleneck for AI-generated PRs — need automated validation
- Onboarding new teams (e.g., India team) requires understanding team-specific conventions and codebase dependencies

### Prior Work
- **Compass** (enterprise KG): Connects Jira tickets → issues → epics → git repos → commits/PRs → deployments
- **VersiCode** [5]: Dataset for version-controlled code generation
- **PA-AKG** (DOE Genesis proposal): Provenance-aware agentic KGs for scientific software — directly informs this proposal's technical approach
- **FOSE 2026** [Cusati & Brown]: Structured knowledge accumulation for software engineering

### Why Academic Research?
- Exploratory — combining agentic KGs with code pattern mining is not yet well-understood
- Need systematic study of how historical patterns improve agent determinism
- Cross-cutting: spans software engineering, AI, knowledge representation, and HCI

## Proposed Approach

Build an **agentic knowledge graph** that:
1. **Mines historical patterns** from eBay's codebase — commit history, PR patterns, code review comments, issue resolutions
2. **Encodes team conventions** — code style, naming conventions, architecture patterns, dependency graphs
3. **Feeds deterministic code agents** — agents query the KG for contextually-relevant patterns before generating code
4. **Supports validation** — KG records expected outcomes/patterns, enabling automated verification of agentic PRs

### Key Components
- **Code Knowledge Graph** — AST-based extraction of APIs, dependencies, and structural patterns from eBay's Java codebase
- **Pattern Evolution** — Track how patterns change across versions (inspired by VersiCode)
- **Agentic Orchestration** — Ranking agents (score candidate solutions by pattern match), generation agents (produce code from KG context), validation agents (check PRs against KG-encoded patterns)
- **Onboarding Module** — Query KG for project-specific conventions, team dependencies, and historical decisions

## Key Contributions
- Novel integration of agentic knowledge graphs with deterministic code generation
- Pattern mining methodology for large-scale enterprise codebases
- Validation framework for agentic PRs using KG-encoded expectations
- Empirical insights from eBay's production codebase

## Feasibility
- **Timeline**: 12 months (standard eRUPT grant period)
- **Resources**: Access to eBay's codebase, Compass KG infrastructure, compute for LLM training/fine-tuning
- **Risks**:
  - Scale of eBay codebase may require sub-sampling (mitigation: focus on specific patterns first — ViewItem/signals as case study)
  - KG extraction reliability (mitigation: staged evaluation with manual validation)
  - Agent determinism may be imperfect (mitigation: define clear metrics for success)

## CFP Question Mapping

| CFP Question | Our Content |
|---|---|
| **Objectives** | KG for deterministic agentic code generation — reduce 2-4 week pattern implementation to minutes; enable trustworthy agentic PRs; accelerate developer onboarding |
| **Previous Work** | Compass KG, VersiCode, PA-AKG (DOE), FOSE 2026 |
| **Methodologies** | AST-based KG construction, pattern mining, agentic orchestration (ranking, generation, validation), contrastive learning for pattern evolution |
| **Impact** | Faster feature development, reduced legacy code burden, trustworthy AI-generated PRs, faster onboarding |
| **Expected Product** | PoC KG + agent pipeline, validation framework, empirical evaluation, publications |
| **Researcher Qualification** | VT team (Brown, Cusati) — expertise in KGs, code generation, and developer tooling |
| **References** | Key papers from prior work |

## References
1. Pan, Shirui, et al. "Unifying large language models and knowledge graphs: A roadmap." IEEE TKDE. 2024.
2. Wu, Tongtong, et al. "Continual learning for large language models: A survey." arXiv:2402.01364. 2024.
3. Wu, Tongtong, et al. "VersiCode: Towards Version-controllable Code Generation." arXiv:2406.07411. 2024.
4. Chen, Shuai, et al. "Exemplar-based Continual Learning via Contrastive Learning." IEEE TAI. 2024.
5. Cusati, Brown, et al. "A Case for Structured Knowledge Accumulation in Software Engineering Research." FOSE 2026.
6. Zhang, Zejun, et al. "Refactoring to Pythonic Idioms: A Hybrid Knowledge-Driven Approach Leveraging Large Language Models." FSE 2024.
7. Su, Yanqi, et al. "Enhancing exploratory testing by large language model and knowledge graph." ICSE 2024.
8. Edge, et al. "From Local to Global: A Graph RAG Approach to Query-Focused Summarization." 2024.

## Acceptance Criteria
- [ ] Design document approved by user
- [ ] CFP question mapping is complete
- [ ] All sections map to available prior work and project notes

## Status
- **Created**: 2026-06-18
- **Last Updated**: 2026-06-18
- **State**: Draft
