# v2 Prior-Art & Novelty Gate — Multi-Repo Agentic Knowledge Graphs

> Deliverable for spec `v2-specification.md` §NFR-001 (fresh novelty gate on the
> **new** v2 claims). Produced 2026-07-07 via 8 targeted Consensus searches
> (facet-by-facet across the 4 new claims) + adversarial synthesis.
> **Overall verdict: `partial-overlap` (unchanged from v1) — reposition as a
> problem-led, empirical 3-technique comparison; do NOT sell the new
> architecture as novel.**
>
> Read alongside `prior-art-analysis.md` (v1 gate, still valid). This document
> only covers the FOUR claims that v2 adds; it does not relitigate the v1
> substrate anchor (provenance KG over the org's own VCS history), which stays
> the defensible kernel and is now merely *extended* to multi-repo.

## TL;DR

The v2 scale-up (single page → whole repo → multi-repo) **does not open
greenfield.** Every new claim lands in an actively-crowded 2025–2026 space.
Enterprise/multi-repo code KGs, per-repo agent memory, cross-repo impact
analysis, and codebase-onboarding tools are all being pursued hard right now —
which is *good* for eRUPT relevance but *bad* for a novelty stack. The safest and
most honest posture (and the one Chris already proposed) is: **the contribution
is the empirical comparison** of how to make a coding agent efficient at
multi-repo understanding — not a claim that graph-of-graphs, memory-bank
traversal, or "agent understands the codebase" are new mechanisms.

| # | New v2 claim | Verdict | One-line rationale |
|---|--------------|---------|--------------------|
| 1 | Graph-of-graphs / multi-graph architecture (Repo + JIRA + Memory-Bank; morph/merge/compose) | **partial-overlap** | Every primitive exists (heterogeneous multi-source code KGs, cross-graph entity resolution, multi-view/task-specific projections, temporal subgraph slicing); the *packaging* is unoccupied but it's assembling known parts. |
| 2 | Per-repository memory-bank traversal by a coding agent | **already-solved (mechanism)** | Persistent memory over repo/commit history for coding agents is the hottest 2025–26 sub-area; the "directory of memory banks" is a packaging distinction, not a new mechanism. |
| 3 | Cross-repository feature synthesis + cross-repo convention validation | **partial-overlap** | Cross-repo impact/breaking-contract detection is crowded (cede); pattern-mining→generation is crowded single-repo; the *intersection* (mine across a multi-repo codebase to synthesize a NEW cross-repo feature) is the least-occupied and most defensible sub-claim. |
| 4 | Codebase-understanding / onboarding acceleration for humans AND agents from commit/PR/issue history | **partial-overlap (shared goal, not a mechanism)** | Both human-onboarding and agent-understanding-from-history are crowded; this is motivation/impact material (strong for eRUPT), not research novelty. |
| 5 | Borrowed memory-systems concepts (§1.7): temporal edge decay (FR-018), multi-resolution L0/L1/L2 nodes (FR-019), spreading-activation retrieval (FR-020) | **already-solved (all three, as general techniques)** | Each is an established 2024–26 LLM-agent-memory / KG-RAG technique with strong exemplars; adopt-and-cite only. Decay-weighting and hierarchical memory are especially crowded. Frame as *adopted design choices + compared candidate techniques*, never as novelty. |

---

## Claim 1 — Graph-of-graphs / multi-graph architecture

**What we're gating:** a *family* of composable graphs (Repo Graph relating
services/repos, JIRA/issue Graph, per-repo Memory-Bank Graph) plus composition
operations — graphs-within-graphs, graphs that "morph/flip" to a task-context
view (issue-view vs feature-view of the same entities), and merging/entity-
resolving nodes across graphs.

**Verdict: `partial-overlap`.**

**The threats (mechanism already exists, in pieces):**

- **[Scalable and Explainable Enterprise Knowledge Discovery Using Graph-Centric
  Hybrid Retrieval](https://consensus.app/papers/details/064df93fff385059b593be9630335704/)**
  (Rao et al., 2025, ArXiv) — the most dangerous neighbor on the *enterprise
  multi-source substrate*: builds a **unified knowledge graph from Jira + Git +
  code + PRs + commit histories + Confluence/wikis**, with query-analysis that
  *dynamically routes* the retrieval strategy. Distinguish: it fuses everything
  into ONE unified graph for retrieval/QA — not a *family* of separately-
  maintained morphing/merging graphs, and it does not generate code.
- **[Improving Issue-PR Link Prediction via Knowledge-Aware Heterogeneous Graph
  Learning](https://consensus.app/papers/details/53684290d25d58089c930b5d4e92f2e8/)**
  (Bai et al., 2024, IEEE TSE) — AIPL models repos, users, issues, PRs and their
  relations as a **heterogeneous graph**, and explicitly builds *task-specific
  heterogeneous graphs* via metapaths. This is the closest analog to "morph to a
  task view." Distinguish: link-prediction target, single-repo framing, no
  memory-bank layer, no code generation.
- **[IssueCourier: Multi-Relational Heterogeneous Temporal Graph Neural Network
  ...](https://consensus.app/papers/details/5880d4e15bbe51f5978b7111378f9945/)**
  (Zhou et al., 2025, IEEE TSE) — heterogeneous graph over issues/developers/
  source files with **temporal slicing into a sequence of subgraphs** to learn
  stage-specific patterns. "Slice the graph by context" is precedented.
- **Generic KG composition is a mature field.** Cross-graph **entity
  resolution / alignment** (the "merging nodes across graphs" operation) has
  dozens of papers — e.g.
  [Collective Multi-type Entity Alignment](https://consensus.app/papers/details/89f943e8d98f5e668a376a1773e36840/)
  (Zhu et al., 2020) and
  [Large-scale Entity Alignment via KG Merging, Partitioning and Embedding](https://consensus.app/papers/details/dc19c91dd8a65040acc554e0f2aab707/)
  (Xin et al., 2022). Multi-relational graph **composition operators** are
  standardized in
  [CompGCN](https://consensus.app/papers/details/320e6d65d9dc5233827738a6ad4f8df0/)
  (Vashishth et al., 2019, 1139 cites).
- **"Morphing/flip by context" ≈ multi-view software modelling**, itself a whole
  subfield:
  [Multi-view approaches for software and system modelling (SLR)](https://consensus.app/papers/details/d33568f285d65c06a4457b445df7f7f6/)
  (Cicchetti et al., 2019) and
  [A feature-based survey of model view approaches](https://consensus.app/papers/details/67a9b8f09c615a93b3e358bc40772650/)
  (Brunelière et al., 2017). Projecting a task-relevant view of shared entities
  is a decades-old idea.

**What no retrieved work does:** package a *Repo + JIRA + per-repo Memory-Bank*
graph-of-graphs, traversed by a coding agent, with explicit morph/merge between
issue-view and feature-view. That specific assembly is unoccupied — **but it is
a composition of known primitives, so it is architecture-novelty, not
mechanism-novelty.** Per NFR-003, every one of these operations needs a
one-sentence "why it earns its place" or a reviewer reads it as architecture for
its own sake. **Recommendation: justify by need (multi-repo scale forces
separation of concerns), do not headline as novel.**

---

## Claim 2 — Per-repository memory-bank traversal by a coding agent

**What we're gating:** a directory of living-documentation "memory banks" across
repositories that a coding agent traverses (alongside PRs and issue tickets) to
determine what changed and why.

**Verdict: `already-solved` (mechanism) — this is the WEAKEST novelty claim.**

Persistent memory for coding agents over repository/commit history is the single
hottest sub-area in the 2025–2026 results. The mechanism is solved; the
"memory-bank directory" is a naming/packaging distinction.

**The threats:**

- **[Prometheus: Unified Knowledge Graphs for Issue Resolution in Multilingual
  Codebases](https://consensus.app/papers/details/fccf9a596b8057fcb0aeb397cba2ebdb/)**
  (Chen et al., 2025) — a **memory-centric coding-agent framework** for
  long-horizon codebase navigation: unified KG + working memory that retains and
  reuses explored context across reasoning steps; SOTA on SWE-bench Verified.
  Directly occupies "agent traverses a persistent structure to understand the
  repo."
- **[Codified Context: Infrastructure for AI Agents in a Complex Codebase](https://consensus.app/papers/details/a23f5ad94e6b5748bb792aaebb1ed38d/)**
  (Vasilopoulos, 2026) — closest to the *memory-bank-directory* idea itself:
  a **hot-memory "constitution"** (conventions/retrieval hooks) + specialized
  domain agents + a **cold-memory knowledge base of on-demand specification
  documents** in a 108k-line system. This is essentially "a directory of living
  docs the agent consults," already built.
- **[Improving Code Localization with Repository Memory](https://consensus.app/papers/details/724f1001a50d5321bcd2392efdc586cc/)**
  (Wang et al., 2025) — augments an agent with memory built from a repo's
  **commit history and linked issues** (functionality summaries of actively
  evolving parts identified via commit patterns) — i.e., "traverse history to
  learn what changed and why," our exact phrasing.
- **[Codebase-Memory: Tree-Sitter-Based Knowledge Graphs for LLM Code
  Exploration via MCP](https://consensus.app/papers/details/2b79ad8913e9540395fc508b0d2f7f09/)**
  (Vogel et al., 2026) — persistent code KG the agent queries instead of
  re-grepping; 10× fewer tokens.
- Plus a dense field of general agent-memory work:
  [A-MEM](https://consensus.app/papers/details/3063d0f87e5057d596424b482a9049c8/)
  (Xu et al., 2025, 651 cites),
  [Memory for Autonomous LLM Agents survey](https://consensus.app/papers/details/c39606478b3c5d80b1d7ed3513145b45/)
  (Du, 2026), and
  [CommitDistill](https://consensus.app/papers/details/e2240df85202500ab39d8e613227bf8b/)
  (Chukkapalli et al., 2026), which mines a repo's git history into **typed
  knowledge units (Facts/Skills/Patterns)** — the "memory bank mined from
  history" idea in miniature.

**Do NOT claim this as novel.** Cede and cite. The only surviving distinction is
*per-repo memory banks composed across a multi-repo codebase* + linking them to
the Repo/JIRA graphs — and that distinction belongs to Claim 1's architecture
argument, not to a standalone novelty.

---

## Claim 3 — Cross-repository feature synthesis + cross-repo convention validation

**What we're gating:** mining commit/PR patterns ACROSS a multi-repo codebase to
design a new feature/task spanning several repos, including cross-repo convention
validation (a change in repo A that breaks an implicit contract with repo B).

**Verdict: `partial-overlap` — cede the impact/contract half; the
synthesis-across-repos half is the most defensible new territory in v2.**

**Sub-claim 3a — cross-repo impact / breaking-contract detection: crowded, cede.**

- **[CCCE: A Continuous Code Calibration Engine for Autonomous Enterprise
  Codebase Maintenance via Knowledge Graph Traversal and Adaptive Decision
  Gating](https://consensus.app/papers/details/8cb947a99f695124a84db39ca517f590/)**
  (Parimi, 2026) — **the single most dangerous v2 neighbor.** Enterprise
  codebases "spanning hundreds of repositories," a **dynamic KG with
  bidirectional traversal** (forward impact propagation + backward test
  adequacy), **cross-repository coordinated changes**, an **adaptive multi-stage
  risk-gating framework**, HITL oversight, and **end-to-end traceability** from
  triggering event to patch. This prints much of our multi-repo + KG-traversal +
  validation-gate + provenance story. **Distinguish hard:** CCCE targets
  *maintenance/calibration* (security freshness, dependency propagation,
  remediation) via risk-tiered patches — NOT open-ended *new feature synthesis*
  from mined historical patterns, and its knowledge is dependency/test structure,
  not org-history-mined change patterns.
- **[Cross Pipeline Code Impact Analysis using Vector Embeddings, Telemetry
  Traces, Graph and LLMs](https://consensus.app/papers/details/77301049ecb3585eaf818a7416e4d5f8/)**
  (Khandelwal et al., 2025) — PR-triggered cross-service impact via a graph +
  telemetry + LLM "Code Impact Score." Occupies "a change in A affects B."
- **[AutoGuard: Reporting Breaking Changes of REST APIs from ... Source Code](https://consensus.app/papers/details/9103511a43315214a9c336b575b95449/)**
  (Lercher et al., 2025) — CI/PR-integrated breaking-change detection across
  services; plus the broader microservice-API-evolution line
  ([Lercher 2023](https://consensus.app/papers/details/fbeed9bae32a5fbf9a95fb17a8ad244f/)).
  "Change in A breaks contract with B" is essentially a solved detection problem.

**Sub-claim 3b — mining patterns → generation: crowded single-repo.**

- **[Learning to Commit: Generating Organic Pull Requests via Online Repository
  Memory](https://consensus.app/papers/details/763ee8c76dd253649058a58e70f057fe/)**
  (Mo Li et al., 2026) — **must-cite, near-twin of our substrate thesis.** Its
  core argument is *literally ours*: "a repository snapshot reveals the final
  state, but not the repository-specific change **patterns by which that state
  was reached**"; it distils earlier commits into reusable skills (coding style,
  internal-API usage, architectural invariants) and conditions PR generation on
  them. **Distinguish:** single-repo, no cross-repo/graph-of-graphs, no
  convention-validation gate.
- **[daVinci-Agency: Unlocking Long-Horizon Agency Data-Efficiently](https://consensus.app/papers/details/9d94bdda62c55d19bacb32ea943df3cf/)**
  (Jiang et al., 2026) — mines structured supervision from **chains-of-PRs**
  (progressive decomposition, refinement trajectories). Confirms PR-history
  mining as an established premise.
- **[MELT: Mining Effective Lightweight Transformations from Pull Requests](https://consensus.app/papers/details/3584d6cffc195eca95153b79940a177a/)**
  (Ramos et al., 2023) — mines migration rules directly from PRs (adjacent to
  PyCraft/Janke from the v1 gate).

**What is genuinely open:** the *intersection* — mining commit/PR patterns
**across a multi-repo codebase** to **synthesize a new feature that spans several
repos**, validated against **cross-repo** conventions, on the org-history
provenance substrate. No retrieved work does synthesis *across* repos from mined
multi-repo patterns (Learning to Commit is single-repo; CCCE is cross-repo but
maintenance-only). **Lead Claim 3 with cross-repo synthesis; cede cross-repo
impact detection to CCCE/Cross-Pipeline/AutoGuard.**

---

## Claim 4 — Codebase-understanding / onboarding acceleration (humans + agents)

**What we're gating:** accelerating onboarding/codebase understanding for BOTH
human developers and coding agents, learned from commit/PR/issue history
(features, style, cross-team collaboration patterns).

**Verdict: `partial-overlap` — this is a shared GOAL, heavily pursued; frame as
motivation/impact, not as a novel mechanism.** (Strong for eRUPT's practical-
application criterion — see NFR-006.)

**The threats (both beneficiary sides are crowded):**

- **[Onboarding in software engineering](https://consensus.app/papers/details/1f71ae1e975d5559a7c44400524a44ba/)**
  (Yates, 2025) and the earlier
  [information-push study](https://consensus.app/papers/details/95a89a148a735d84963286995b481bcf/)
  (Yates et al., 2019) — **grounds our exact framing:** identifies that
  onboarding needs **Temporal and Rationale views** of code (what changed, what
  is changing, why) beyond Structural/Algorithmic — i.e., "understand history and
  the *why*." Use as the human-side motivation anchor; distinguish that we
  *auto-mine* those views from VCS rather than eliciting them from an expert.
- **[A Multi-agent Onboarding Assistant based on LLMs, RAG, and Chain-of-Thought
  (Onboarding Buddy)](https://consensus.app/papers/details/b1f8bc3376585d02b0138cf383534806/)**
  (Ionescu et al., 2025, FSE) — agent-based onboarding assistant giving NL
  explanations/code insights. Occupies "AI accelerates human onboarding."
- **[AI-Guided Exploration of Large-Scale Codebases](https://consensus.app/papers/details/39d153ad1bbf5cb6afec86a29e8875fc/)**
  (Alebachew, 2025) — reiterates the 70%-of-time-on-comprehension stat and the
  onboarding/feature-development framing (a motivation cite, complements CCT5).
- **[Ontology-Based Software Graphs for Supporting Code Comprehension During
  Onboarding](https://consensus.app/papers/details/744620b4842c5015b3a74638a4503f8b/)**
  (Nagel et al., 2021) — graph-based onboarding comprehension aid; a graph over
  code for onboarding is not new.
- Agent-side understanding: **[How to Understand Whole Software Repository?
  (RepoUnderstander)](https://consensus.app/papers/details/76591306c5685083b7dcc876d3a14eda/)**
  (Ma et al., 2024) condenses a repo into a KG for agent comprehension; plus
  Prometheus / Codebase-Memory (Claim 2).

**Takeaway:** "make onboarding/understanding faster for humans and agents" is a
widely-shared objective, not a claimable novelty. It is our **impact story** and
should lead the eRUPT Impact section with the v1 industry numbers (DeputyDev,
Akalanka, AKUs) — not be presented as research novelty.

---

## Claim 5 — Borrowed memory-systems concepts (§1.7): decay / multi-resolution / spreading activation

**What we're gating:** the three concepts §1.7 adopts to sharpen the substrate
story — (FR-018) **temporal edge decay** (edges weaken over time unless
reinforced), (FR-019) **multi-resolution memory nodes** (L0 compressed / L1
reasoning / L2 full body), and (FR-020) **spreading-activation retrieval**
(activation diffuses across graph edges vs. similarity/RAG). The spec already
says these are *borrowed and attributed*, not sold as ours — the gate confirms
that posture is **mandatory**: all three are already-solved general techniques.

**Verdict: `already-solved` for all three (as general mechanisms).** Adopt and
cite; add spreading activation and topology as *axes of the FR-014 comparison*.

**FR-018 — temporal / decay-weighted memory: heavily crowded.**

- **[Zep: A Temporal Knowledge Graph Architecture for Agent Memory](https://consensus.app/papers/details/acb7c16242e750a8b5e3c8cbe18c647d/)**
  (Rasmussen et al., 2025, 213 cites) — the reference temporal-KG agent-memory
  system (Graphiti engine), enterprise-framed. Adopt-cite for FR-018.
- **[Not All Memories Age the Same: Autodiscovery of Adaptive Decay in Knowledge
  Graphs](https://consensus.app/papers/details/e65821f8e3bf5599a8f119d52779d5a0/)**
  (Karhade, 2026) — decay surfaces (velocity/volatility) per knowledge type; and
  **[FadeMem: Biologically-Inspired Forgetting for Efficient Agent Memory](https://consensus.app/papers/details/1d20785fbf94548db325cf84e26ebc0f/)**
  (Wei et al., 2026), **[DynaKG: Dynamic Knowledge Graph Attention With Learnable
  Temporal Decay](https://consensus.app/papers/details/b57c41e88dba5d8b89300a86e311274a/)**
  (Chomba et al., 2025). "Edges weaken over time unless reinforced" is textbook.
  **WATCH-OUT: do not headline a decay-weighted history KG as novel.**

**FR-019 — multi-resolution / hierarchical memory nodes: heavily crowded.**

- **[Hierarchical Memory for High-Efficiency Long-Term Reasoning in LLM Agents
  (H-MEM)](https://consensus.app/papers/details/ba5f4e3a0fa05734b343dea9214c988f/)**
  (Sun et al., 2025) — multi-level memory by semantic-abstraction degree, index-
  routed coarse→fine retrieval. Exactly L0/L1/L2.
- **[HyMem](https://consensus.app/papers/details/362997578ec350c29d0030753378cebe/)**
  (Zhao et al., 2026, dual-granular summary-vs-deep, on-demand drill-down),
  **[HORMA](https://consensus.app/papers/details/9bd6aec8de6f5ba3b09732912ff04f44/)**
  (Hsu et al., 2026, summaries linked to raw trajectories),
  **[G-Memory](https://consensus.app/papers/details/99621a9c941857cdb26123c4558b7f12/)**
  (Zhang et al., 2025, 64 cites, three-tier insight/query/interaction graph), and
  **[xMemory](https://consensus.app/papers/details/ff5f689844445b358a144a568c944995/)**
  (Hu et al., 2026, decouple-then-aggregate, top-down expansion). The
  summary→detail hierarchy is a solved pattern. **WATCH-OUT: FR-019 must read as
  "we adopt hierarchical memory (cite)," not "we invent it."**

**FR-020 — spreading-activation retrieval: exists, not yet for code.**

- **[Leveraging Spreading Activation for Improved Document Retrieval in
  Knowledge-Graph-Based RAG Systems](https://consensus.app/papers/details/4246c52fb22754ef9c4b73ac4c31dfdb/)**
  (Pavlović et al., 2025) — activation-diffusion retrieval over an auto-built KG,
  beating similarity RAG on multi-hop QA *without* LLM-guided traversal. This is
  the modern instantiation FR-020 needs (pair with Collins & Loftus 1975).
  **Partial-overlap:** the algorithm is off-the-shelf; our only contribution is
  *evaluating it as a candidate retrieval mode on a code-history graph* — so it
  belongs in the FR-014 comparison as a baseline, not as an invention.

**Net for §1.7:** these three concepts are a **strength for the writing** (they
make "a dynamic, decay-weighted, multi-resolution history KG" a crisper story
than a flat static graph) but a **liability if over-claimed.** Cite Zep +
H-MEM/HyMem + Pavlović (+ Collins & Loftus 1975) as the sources; convert
"spreading activation vs. similarity/RAG vs. graph query" and "single-KG vs.
graph-of-graphs vs. memory-bank" into the **research-comparison axes** (FR-014),
which turns crowded prior art into our evaluation design rather than a novelty
fight.

---

## Overall v2 verdict & how it should shape the framing

**Overall: `partial-overlap` (consistent with v1).** The multi-repo scale-up
adds surface area but no greenfield: all four new claims sit in dense 2025–2026
literature. Two neighbors did not exist (or were not surfaced) at v1 time and are
now the sharpest threats: **CCCE** (cross-repo KG traversal + gating +
traceability) and **Learning to Commit / Online Repository Memory** (history-
patterns→grounded-PR, which restates our substrate thesis almost verbatim). The
defensible kernel is unchanged and must be reaffirmed: **a provenance-aware KG
mined from the org's OWN version-control history (commits + PRs + reviews) as the
shared substrate for both generation and convention-validation** — now extended
to multi-repo.

### Crowded vs. open (be explicit in the draft)

- **Crowded — mechanism exists, must cede & cite:**
  - Enterprise/multi-source code KGs (Rao 2025, Prometheus, KGCompass, AIPL).
  - Per-repo agent memory over history (Claim 2 — Prometheus, Codified Context,
    Wang 2025, Codebase-Memory, CommitDistill). **Weakest claim; do not headline.**
  - Cross-repo impact / breaking-contract detection (Claim 3a — CCCE,
    Cross-Pipeline, AutoGuard, Lercher).
  - Onboarding/comprehension acceleration as a goal (Claim 4 — Onboarding Buddy,
    Yates, RepoUnderstander).
  - **All three §1.7 memory concepts (Claim 5):** temporal decay (Zep, FadeMem,
    DynaKG), multi-resolution memory (H-MEM, HyMem, G-Memory), spreading
    activation (Pavlović 2025). **Adopt-and-cite only — do not headline.**
- **Open — problem largely unoccupied, safe to stake:**
  - **Cross-repo feature *synthesis*** from mined multi-repo commit/PR patterns +
    **cross-repo** convention validation on the org-history substrate (Claim 3b∩3a
    intersection). Least-occupied.
  - **The empirical comparison itself** (Chris's framing, FR-013/FR-014): nobody
    has run a head-to-head of KG topology (single unified KG vs. graph-of-graphs
    vs. memory-bank traversal) × backend (Neo4j vs. Gremlin vs. Auto Graph) for
    *coding-agent multi-repo-understanding efficiency*. Making the **comparison**
    the contribution sidesteps every mechanism-novelty fight above.

### Framing moves for the v2 draft

1. **Lead with the PROBLEM and the empirical-comparison posture, not the
   architecture.** Position v2 as "we evaluate ~3 techniques for making a coding
   agent efficient at multi-repo understanding and report what works and why"
   (FR-013). This is the strongest defensible novelty and matches the notes.
2. **Reaffirm the v1 kernel** (org-history provenance KG as shared substrate for
   generation + validation) as the through-line; v2 = same idea at multi-repo
   scale. Do not re-derive it — cite the v1 gate.
3. **Soften Claims 1, 2, 4 to supporting roles.** Graph-of-graphs = justified by
   multi-repo scale (NFR-003), not sold as novel. Memory-bank traversal = an
   *implementation option being compared*, explicitly citing Codified Context /
   Prometheus / Wang 2025. Onboarding = impact/motivation, not novelty.
4. **Stake the sharpest new claim on cross-repo synthesis + cross-repo
   convention validation** (Claim 3b), and pre-empt CCCE with one sentence:
   *"unlike autonomous maintenance/calibration engines (CCCE), we synthesize
   new cross-repo features from mined historical change patterns and validate
   them against team conventions, not just dependency/test structure."*
5. **Pre-empt Learning to Commit explicitly.** It states our snapshot-vs-history
   insight; distinguish on multi-repo scope + graph-of-graphs substrate +
   convention gate, and cite it as convergent evidence the premise is sound.
6. **Keep the validation gate "support, not replacement"** (carry over v1 /
   Heander framing) and generalize it to cross-repo contracts.

---

## New citation candidates (real, Consensus-surfaced — extend `references.json`)

Priority order for the reference store. Metadata as returned by Consensus; verify
via `review-agent` §4A before adding (several are very recent / arXiv-only or
"Unknown Journal").

| Suggested id | Paper | Year / venue | Role in v2 |
|--------------|-------|--------------|-----------|
| `ccce2026` | [CCCE: A Continuous Code Calibration Engine ... via Knowledge Graph Traversal and Adaptive Decision Gating](https://consensus.app/papers/details/8cb947a99f695124a84db39ca517f590/) (Parimi) | 2026, ArXiv | **Must-distinguish-from** — closest cross-repo KG-traversal + gating + traceability (maintenance, not feature synthesis). |
| `learn2commit2026` | [Learning to Commit: Generating Organic Pull Requests via Online Repository Memory](https://consensus.app/papers/details/763ee8c76dd253649058a58e70f057fe/) (Mo Li et al.) | 2026, ArXiv | **Must-distinguish-from** — restates snapshot-vs-history substrate thesis; single-repo. |
| `prometheus2025` | [Prometheus: Unified Knowledge Graphs for Issue Resolution in Multilingual Codebases](https://consensus.app/papers/details/fccf9a596b8057fcb0aeb397cba2ebdb/) (Chen et al.) | 2025, ArXiv | Mechanism cede — memory-centric multi-agent coding over a unified code KG. |
| `enterpriseKG2025` | [Scalable and Explainable Enterprise Knowledge Discovery Using Graph-Centric Hybrid Retrieval](https://consensus.app/papers/details/064df93fff385059b593be9630335704/) (Rao et al.) | 2025, ArXiv | Closest on enterprise multi-source substrate (Jira+Git+PRs); distinguish: single unified graph, retrieval not generation. |
| `codifiedcontext2026` | [Codified Context: Infrastructure for AI Agents in a Complex Codebase](https://consensus.app/papers/details/a23f5ad94e6b5748bb792aaebb1ed38d/) (Vasilopoulos) | 2026, ArXiv | Closest to the memory-bank-directory idea (hot/cold memory + spec docs). Claim 2 cede. |
| `aipl2024` | [Improving Issue-PR Link Prediction via Knowledge-Aware Heterogeneous Graph Learning](https://consensus.app/papers/details/53684290d25d58089c930b5d4e92f2e8/) (Bai et al.) | 2024, IEEE TSE | Claim 1 — heterogeneous graph of GitHub sources + task-specific graphs (morph analog). |
| `yates2025onboarding` | [Onboarding in software engineering](https://consensus.app/papers/details/1f71ae1e975d5559a7c44400524a44ba/) (Yates) | 2025 | Claim 4 human-side anchor — Temporal + Rationale views ("what changed and why"). |
| `repomem2025` | [Improving Code Localization with Repository Memory](https://consensus.app/papers/details/724f1001a50d5321bcd2392efdc586cc/) (Wang et al.) | 2025, ArXiv | Claim 2 — commit-history-as-memory for agents. |
| `crosspipeline2025` | [Cross Pipeline Code Impact Analysis using Vector Embeddings, Telemetry Traces, Graph and LLMs](https://consensus.app/papers/details/77301049ecb3585eaf818a7416e4d5f8/) (Khandelwal et al.) | 2025 | Claim 3a cede — cross-service PR impact analysis. |
| `autoguard2025` | [AutoGuard: Reporting Breaking Changes of REST APIs from Java Spring Boot Source Code](https://consensus.app/papers/details/9103511a43315214a9c336b575b95449/) (Lercher et al.) | 2025, SANER | Claim 3a cede — CI/PR breaking-change detection (cross-repo convention validation prior art). |
| `davinci2026` | [daVinci-Agency: Unlocking Long-Horizon Agency Data-Efficiently](https://consensus.app/papers/details/9d94bdda62c55d19bacb32ea943df3cf/) (Jiang et al.) | 2026, ArXiv | Claim 3b premise — chain-of-PR mining (optional). |
| `onboardingbuddy2025` | [A Multi-agent Onboarding Assistant based on LLMs, RAG, and Chain-of-Thought](https://consensus.app/papers/details/b1f8bc3376585d02b0138cf383534806/) (Ionescu et al.) | 2025, FSE | Claim 4 — agentic onboarding assistant (optional). |
| `zep2025` | [Zep: A Temporal Knowledge Graph Architecture for Agent Memory](https://consensus.app/papers/details/acb7c16242e750a8b5e3c8cbe18c647d/) (Rasmussen et al.) | 2025, ArXiv (213 cites) | **Adopt-cite** for FR-018 temporal edge decay. |
| `hmem2025` | [Hierarchical Memory for High-Efficiency Long-Term Reasoning in LLM Agents (H-MEM)](https://consensus.app/papers/details/ba5f4e3a0fa05734b343dea9214c988f/) (Sun et al.) | 2025 | **Adopt-cite** for FR-019 multi-resolution nodes (alt: HyMem / G-Memory). |
| `spreadact2025` | [Leveraging Spreading Activation for Improved Document Retrieval in KG-Based RAG Systems](https://consensus.app/papers/details/4246c52fb22754ef9c4b73ac4c31dfdb/) (Pavlović et al.) | 2025, ArXiv | **Adopt-cite** for FR-020 (pair with Collins & Loftus 1975); a compared retrieval mode. |
| `commitdistill2026` | [CommitDistill: A Lightweight Knowledge-Centric Memory Layer for Software Repositories](https://consensus.app/papers/details/e2240df85202500ab39d8e613227bf8b/) (Chukkapalli et al.) | 2026 | Claim 2 cede — mines git history into typed knowledge units (Facts/Skills/Patterns). |
| `mvkg2024` | [A Survey on Multi-View Knowledge Graph: Generation, Fusion, Applications](https://consensus.app/papers/details/77f847c4b007535f95877ac11076391b/) (Yang et al.) | 2024 | Claim 1 — grounds "context-morphing views" as an established multi-view-KG concept. |
| `akalanka2025` | [AI Powered Integrated Code Repository Analyzer for Efficient Developer Workflow](https://consensus.app/papers/details/6019f3efd1f25bd69e5a811be7045e85/) (Akalanka et al.) | 2025, SCSE | **Motivate** — 50–60% less senior-dev involvement, −90% doc effort (also in v1). |
| `akus2026` | [Knowledge Activation: AI Skills as the Institutional Knowledge Primitive (AKUs)](https://consensus.app/papers/details/45884eb39b9255389be8f3cc922895df/) (Bakal) | 2026, ArXiv | **Motivate + distinguish** — Yahoo deployment; closest-on-problem (also in v1). |

**Trim guidance:** for a 2–3 page proposal, add at most **CCCE, Learning to
Commit, Prometheus, Rao 2025, Codified Context** (the 5 must-distinguish/cede
cites) plus **Yates** for the onboarding framing. The rest are held as
`candidatesNotYetCited`.

---

## Method notes

- 8 successful Consensus searches (query-text only, no filters, per protocol),
  facet-by-facet across the 4 claims. The connector rate-limited aggressively
  (~1 successful call per ~30–40 s window regardless of batching), so calls were
  spaced with waits; each returned the full top-19/20.
- Queries: (1) graph-of-graphs composable code KG; (2) multi-graph composition /
  entity resolution / node merging; (3) task-context graph view switching
  (issue-view vs feature-view); (4) LLM-agent persistent memory / documentation
  over repo history; (5) cross-repo breaking-contract detection; (6) mining
  commit/PR history to synthesize a multi-service feature; (7) onboarding /
  codebase comprehension from repo history; (8) heterogeneous KG integrating
  issue-tracker + commits + code + deps across repos.
- **Second pass (2026-07-07, added Claim 5 / §1.7 coverage):** 8 further
  Consensus searches specifically targeting the borrowed memory-systems concepts
  and newer history-mining work — (a) graph-of-graphs code-KG composition;
  (b) per-repo memory-bank traversal / onboarding; (c) cross-repo feature dev with
  KG/agents; (d) code-history KG for codegen (2025+); (e) temporal/decay-weighted
  KG & agent memory; (f) spreading-activation retrieval over KGs vs. RAG;
  (g) multi-resolution / hierarchical LLM-agent memory; (h) developer-onboarding
  via mined history. Confirmed FR-018/019/020 are already-solved general
  techniques (Zep, H-MEM/HyMem, Pavlović) and surfaced newer history-mining
  threats (Learning to Commit, CommitDistill, Rao 2025 enterprise KG). Verdict
  unchanged; Claim 5 + associated cites added above.
- All papers above are real and Consensus-surfaced; metadata is as returned and
  must pass `review-agent` §4A before entering `references.json`.
