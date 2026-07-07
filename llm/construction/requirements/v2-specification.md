# Proposal v2 Specification: Multi-Repo Agentic Knowledge Graphs

> **Purpose.** Specify what changes for **version 2** of the eBay eRUPT proposal.
> Source inputs: `files/preliminary-meeting-notes.md` (Jason + Chris),
> `llm/memory-bank/*`, and the validated v1 framing
> (`prior-art-analysis.md`). This is a *planning/spec* document, not the draft
> itself — it defines scope, requirements, and acceptance criteria for the v2
> rewrite of `proposal/main.tex`.
>
> **The one-line shift:** v1 scoped the target to a **single ViewItem page in a
> single repository**. v2 scales the target to the **entire codebase**, where
> *codebase = one GitHub repository*, and an eBay feature **generally spans more
> than one repository.** The core ideas (a provenance KG mined from the org's own
> version-control history, used to generate and validate changes) **stay the
> same**; the unit of analysis grows from one page to a cross-repository system.

---

## 0. What stays the same (carried over from v1)

Priority: **Must-keep.** These are settled and validated — do not relitigate.

- Provenance-aware knowledge graph mined from the org's **own version-control
  history** (commits, PRs, code reviews) as the substrate. Novelty anchor.
- Problem-led framing; determinism is a *supporting* property, not the headline.
- Validation gate **supports reviewers, it does not replace them**.
- eRUPT 7-section structure; `.docx` template; Sept 21 2026 deadline; $120K.
- Team + engagement structure (PI Brown, GRA Cusati, Co-I Periyathambi).
- The §4A-verified reference store (`references.json`) is reused and extended,
  not rebuilt.

---

## 1. Functional Requirements — what v2 must cover

### 1.1 Problem statement (expanded)
- **FR-001 (Must).** State the unifying problem from the notes: *"How can we make
  a coding agent efficient at genuinely understanding a large, multi-repository
  codebase — using its commits, PRs, and JIRA history — so that onboarding,
  cross-repo feature development, and code review are faster?"*
- **FR-002 (Must).** Name the three concrete blockers the notes call out, and tie
  each to the proposed work:
  1. **Onboarding cost** on massive/legacy codebases (humans *and* agents).
  2. **Costly feature development** — a feature can take a year+ including A/B
     testing, and spans multiple repositories/teams.
  3. **Code review / approval bottleneck** — the major blocker; goal is fewer
     review cycles and faster review.
- **FR-003 (Should).** Frame the beneficiary as **both the human developer and
  the coding agent** ("teach each new codebase faster"), not the agent alone.

### 1.2 Scale-up: single page → whole codebase → multi-repo
- **FR-004 (Must).** Redefine the unit of analysis: *codebase = a GitHub
  repository*; the KG now models an **entire repository**, not one page/handler.
- **FR-005 (Must).** Model **cross-repository features**: a single feature/JIRA
  epic touches multiple repositories/services. The KG must represent and traverse
  these inter-repo relationships (service-to-service, shared APIs, call/dep edges).
- **FR-006 (Should).** Preserve the ViewItem signal as a *worked micro-example*
  inside the larger story, but demote it from "the scope" to "an illustration of
  a pattern that, at scale, recurs across repos."

### 1.3 Multiple, composable graphs (the v2 architecture)
- **FR-007 (Must).** Replace the single monolithic KG with a **family of graphs**
  (from the notes):
  - **Repo Graph** — relates services/repositories to each other (dependencies,
    shared libraries, cross-team ownership, call relationships).
  - **JIRA Graph** — work items → epics → features, their links to commits/PRs,
    and out to the external resources they cite.
  - **Memory-Bank Graph** — per-repo living documentation (the constellize
    memory-bank idea applied *per repository*), traversable by an agent. Nodes are
    stored at **three resolutions** — compressed summary / reasoning context /
    full body (see FR-019) — so an agent scans cheaply then drills down.
- **FR-008 (Should).** Specify **graph composition** operations named in the
  notes, at proposal-appropriate depth (concept + why it matters, not
  implementation): *graphs within graphs*, *graphs that morph/flip based on
  context* (e.g. a JIRA-centric view vs. a feature-centric view of the same
  entities), and *merging graph nodes* across graphs (entity resolution: the same
  service/commit/ticket appearing in more than one graph).
- **FR-009 (Should).** Describe **context-driven views**: the agent projects the
  relevant graph(s) for the task at hand (onboarding vs. feature design vs.
  review) rather than querying one giant graph.

### 1.4 Agent behaviors over the graphs
- **FR-010 (Must).** Agent **traverses** memory banks, PRs, and JIRA to determine
  *what changed and why* — Chris's stated novelty candidate ("directory of memory
  banks across repos that a coding agent can traverse").
- **FR-011 (Must).** Agent **mines commit/PR patterns** across the codebase to
  learn features, coding style, and cross-team collaboration patterns, and uses
  them when designing a **new feature or task**. Pattern relevance is
  **time-weighted via edge decay** (see FR-018) so recent conventions outrank
  stale ones.
- **FR-012 (Should).** Convention-validation gate generalizes from one repo to
  **cross-repo conventions** (a change in repo A that breaks an implicit contract
  with repo B).

### 1.5 Research design (Chris's framing) — **HEADLINE, locked 2026-07-07**
> **Decision (validated by `v2-prior-art-analysis.md`, verdict `partial-overlap`):**
> the v2 novelty is **the empirical comparison itself**, staked on **cross-repo
> synthesis** — *not* the graph structure. The novelty gate showed every mechanism
> (graph-of-graphs, memory-bank traversal, decay/multi-resolution/spreading-
> activation) is already crowded 2025–26 prior art; the one thing no one has done
> is a head-to-head of *how to make a coding agent efficient at multi-repo
> understanding*. Topology is demoted to justified-by-scale architecture; backend
> is a footnote.

- **FR-013 (Must).** Position v2 explicitly as a **research problem, not an
  immediate eBay deployment**: Jason evaluates **3 candidate techniques** for
  making the coding agent most efficient at multi-repo codebase understanding,
  and reports back which works best and why — deliverable eBay can learn from and
  extend. **This empirical comparison IS the contribution** (it sidesteps every
  crowded-mechanism novelty fight — see prior-art analysis).
- **FR-014 (Must).** The **headline comparison axis = retrieval / traversal
  strategy**: **(a) graph queries vs. (b) similarity / RAG vs. (c)
  spreading-activation** (FR-020) over the code-history graph. This is the one
  clean, measurable 3-way benchmark that maps directly onto Chris's "3 techniques"
  framing. Secondary axes are held as *implementation choices, not headline
  experiments*: topology (single-KG vs. graph-of-graphs vs. memory-bank
  traversal) is justified by multi-repo scale (NFR-003); backend (Neo4J vs.
  Gremlin vs. Auto Graph Framework) is an implementation footnote.
- **FR-014a (Must).** Pair the comparison with the **sharpest stake-able novel
  claim** the gate left open: **cross-repo feature *synthesis* from mined
  multi-repo commit/PR patterns + cross-repo convention validation** (Claim 3b,
  FR-005/FR-011/FR-012). Pre-empt the two nearest neighbors in one sentence each:
  *CCCE* (cross-repo KG traversal, but maintenance/calibration — not new-feature
  synthesis) and *Learning to Commit* (our snapshot-vs-history thesis, but
  single-repo).
- **FR-015 (Must — promoted from Nice).** State a concrete **evaluation signal**
  for "agent understands the codebase better," or the 3-way comparison has nothing
  to compare *on*. Candidate metrics (pick 1–2 in drafting): cross-repo
  feature-scaffold accuracy, onboarding-task success rate, review-cycle /
  review-comment reduction. **Open Question #4 — needs Jason's pick before draft.**

### 1.6 eBay alignment & practical hooks
- **FR-016 (Must).** Keep the Compass (eBay enterprise KG) relationship; position
  the multi-graph approach as *extending* Compass with code-level + memory-bank
  knowledge tickets don't capture.
- **FR-017 (Should).** Note operational reality from the notes: eBay laptop +
  funding follow **contract signing**; frame the plan so early research phases
  don't hard-depend on internal eBay access.

### 1.7 Memory-systems concepts (borrowed, attributed to academic sources)
> Three design choices adopted from spreading-activation memory systems (surfaced
> via a review of Constellation Engine, 2026-07-07). **The product itself is not
> cited** — it's a local-first single-agent identity project, not peer-reviewed or
> enterprise work. The *concepts* are grounded in real literature (spreading
> activation → Collins & Loftus 1975; and modern LLM-agent memory work), and that
> is what v2 cites. These sharpen the novelty story: a *dynamic, decay-weighted,
> multi-resolution* history KG is a crisper claim than a flat static graph.

- **FR-018 (Should) — Temporal edge decay.** Edges in the code-history graph
  **weaken over time unless reinforced** by recent activity, so the substrate
  reflects *current* team conventions rather than accumulated historical noise.
  Rationale: "a graph that never forgets is a graph that drowns"; directly
  strengthens FR-011's pattern mining and differentiates us from static-KG prior
  art. *Needs cite: temporal/decay memory + spreading activation.*
- **FR-019 (Should) — Multi-resolution memory nodes (L0/L1/L2).** Memory-Bank
  Graph nodes carry three resolutions — **compressed summary (L0) / reasoning
  context (L1) / full body (L2)** — letting the agent traverse broadly at low cost
  and expand only where relevant. Rationale: makes cross-repo memory-bank
  traversal (FR-010) tractable at codebase scale. *Needs cite: hierarchical /
  multi-resolution memory or context compression.*
- **FR-020 (Should) — Spreading-activation retrieval.** Offer **activation
  diffusion across graph edges** as a retrieval mode — starting from the task
  prompt, activation spreads along relationships to surface related patterns —
  as an alternative to similarity/RAG search and to plain graph queries.
  Rationale: path-dependent recall suits the graph-of-graphs; **added as a fourth
  candidate technique in the FR-014 comparison.** *Needs cite: spreading
  activation (Collins & Loftus 1975) + a modern agent-memory instantiation.*

---

## 2. Non-Functional Requirements — proposal quality attributes

### 2.1 Novelty & prior-art — **GATE COMPLETE (2026-07-07)**
- **NFR-001 (Must — SATISFIED).** Novelty gate ran (8+8 Consensus searches,
  adversarial synthesis) → `v2-prior-art-analysis.md`. **Verdict:
  `partial-overlap`** (consistent with v1). Findings that bind the draft:
  - Every new *mechanism* is crowded 2025–26 prior art — graph-of-graphs
    (Rao 2025, AIPL, IssueCourier), memory-bank traversal (Prometheus, Codified
    Context, Wang 2025 — **already-solved, weakest claim**), decay /
    multi-resolution / spreading-activation (Zep, H-MEM, Pavlović — all
    already-solved). **Cede and cite; do not headline.**
  - Two sharpest neighbors to pre-empt: **CCCE** (Parimi 2026 — cross-repo KG
    traversal + gating, but *maintenance* not synthesis) and **Learning to
    Commit** (Mo Li 2026 — our snapshot-vs-history thesis, but *single-repo*).
  - **Open territory (safe to stake):** cross-repo feature *synthesis* from mined
    multi-repo patterns (Claim 3b) + **the empirical comparison itself** (FR-013/
    014). Novelty rests here — see §1.5 headline decision.

### 2.2 Feasibility & scope discipline
- **NFR-002 (Must).** v2 must not read as "boil the ocean." Bigger target →
  greater over-reach risk. Keep a **scoped, staged plan** (e.g. a bounded set of
  ~10 related repos containing one realistic cross-repo feature end to end) even
  while the *vision* is codebase-wide. **Ramesh's input: a single eBay feature
  typically touches/needs 5+ repositories** — so the case-study bound is ~10, not
  2–3, to hold a full feature.
- **NFR-003 (Should).** Every new mechanism (morphing graphs, node merging) needs
  a one-sentence *why it earns its place* — reviewers penalize architecture for
  its own sake.

### 2.3 Format & length
- **NFR-004 (Must).** Still fits the eRUPT template (~2–3 pages of content).
  Expansion of *ambition* must not balloon the page count — tighten prose, don't
  add sections.
- **NFR-005 (Must).** Compiles clean from `proposal/main.tex`; citation markers
  stay sequential and §4A-verified.

### 2.4 eBay relevance
- **NFR-006 (Must).** Every claim maps to an eBay-stated pain (onboarding, year+
  feature cycles, review bottleneck, multi-repo features). Impact section leads
  with these.

---

## 3. System Constraints

- **C-1.** Deliverable = the eBay `.docx` template; LaTeX is the working draft.
- **C-2.** Deadline **September 21, 2026**; Ramesh out after **July 8** (open
  items: VP name, $120K sanity-check, terminology).
- **C-3.** IP: eBay expects royalty-free rights min.; permissive OSS possible.
- **C-4.** **DOE Genesis work stays uncited** (separate venue, per PR #1).
- **C-5.** Terminology (signal / ViewItem / signal handler) still eBay-unverified;
  v2 leans less on it since the scope is now whole-codebase.
- **C-6.** No dependency on internal eBay access for the research plan's early
  phases (laptop/funding follow contract).

---

## 4. Acceptance Criteria (v2 draft is "done" when…)

- **AC-1.** Problem statement leads with the multi-repo, whole-codebase framing
  and the three named blockers (FR-001, FR-002).
- **AC-2.** Scope explicitly defines *codebase = repository* and models
  **cross-repository features** (FR-004, FR-005).
- **AC-3.** The multi-graph architecture (Repo / JIRA / Memory-Bank graphs) and
  at least the *concept* of graph composition (within/morph/merge) appear, each
  with a one-line justification (FR-007, FR-008, NFR-003).
- **AC-4.** Memory-bank-traversal + cross-repo pattern mining are present as the
  named novelty candidates and **survive a fresh novelty gate** (FR-010, FR-011,
  NFR-001).
- **AC-5.** The proposal reads as a **3-technique research comparison on the
  retrieval axis** (graph query vs. RAG vs. spreading activation), staked on
  **cross-repo synthesis**, with ≥1 measurable "agent understands better" signal,
  and pre-empts CCCE + Learning to Commit in one sentence each (FR-013, FR-014,
  FR-014a, FR-015).
- **AC-6.** Still fits the template, compiles clean, references §4A-verified
  (NFR-004, NFR-005).
- **AC-7.** All open questions (§5) are either resolved or explicitly flagged as
  team/Ramesh/Dr. A follow-ups — none silently dropped.

---

## 5. Open Questions

**Resolved 2026-07-07:**
- ~~**Q1 — Which 3 techniques?**~~ **LOCKED (§1.5):** headline axis = **retrieval /
  traversal** (graph query vs. RAG vs. spreading activation), staked on cross-repo
  synthesis. Topology = justified-by-scale architecture; backend = footnote.
  Validated by `v2-prior-art-analysis.md`.
- ~~**Novelty gate**~~ **DONE:** verdict `partial-overlap` (NFR-001).

**Still open (need a human decision before/while drafting):**
1. **Q2 — How far to push "morphing/merging graphs"** in a 2–3 page proposal?
   Recommend: one paragraph + one figure; keep depth for the full research plan.
   *Decision: team.* (Gate reinforces: it's crowded prior art — soft-pedal it.)
2. **Q4 — Evaluation metric** (FR-015, now Must): pick 1–2 concrete signals for
   "agent understands the codebase better" (cross-repo scaffold accuracy /
   onboarding-task success / review-cycle reduction). **Blocks drafting the
   experiment section.** *Decision: Jason.*
3. **Q3 — Dr. A meeting** — does NOT gate drafting (per Jason 2026-07-07); Jason
   will share the completed proposal with him. *No blocker.*
4. **Q5 — Reference trim** — 18 candidates surfaced (§ below); for 2–3 pages add
   the ~6 must-cite, hold the rest. Needs §4A verification pass. *Owner: review-agent.*

---

## 6. Execution order (for the v2 rewrite) — progress-tracked

1. ~~**Novelty gate**~~ ✅ done → `v2-prior-art-analysis.md` (verdict partial-overlap).
2. ~~**Resolve Q1 (the axis)**~~ ✅ locked → retrieval axis + cross-repo synthesis (§1.5).
3. **Extend `references.json`** with the ~6 must-cite v2 papers + re-run §4A
   verification (`review-agent`). ← **NEXT (teed up, see §7).**
4. **Jason picks the evaluation metric** (Q4) — needed for the experiment section.
5. **Draft** the v2 scope + problem + comparison + impact sections against the ACs.
6. Compile-check; self-review → `review-agent` → PR for team review.

---

## 7. Teed-up: reference-store extension (the immediate next build step)

From `v2-prior-art-analysis.md`, add these **6 must-cite** papers to
`references.json` and run the §4A verification protocol (exists / no-hallucination
/ correct-citation) before they enter `main.tex`. The remaining 12 candidates stay
in a `candidatesNotYetCited` bucket for Chris's trim.

| id | Paper (year) | Role in v2 draft |
|----|--------------|------------------|
| `ccce2026` | CCCE (Parimi 2026) | **Distinguish** — cross-repo KG traversal + gating, but *maintenance* not synthesis. |
| `learn2commit2026` | Learning to Commit (Mo Li 2026) | **Distinguish** — restates snapshot-vs-history thesis; single-repo. |
| `prometheus2025` | Prometheus (Chen 2025) | Cede — memory-centric coding over a unified code KG. |
| `enterpriseKG2025` | Enterprise Knowledge Discovery (Rao 2025) | Closest enterprise multi-source substrate (Jira+Git+PRs). |
| `codifiedcontext2026` | Codified Context (Vasilopoulos 2026) | Cede — the memory-bank-directory idea, already built. |
| `yates2025onboarding` | Onboarding in SE (Yates 2025) | Impact/motivation anchor — Temporal + Rationale views. |

**Verification caveat:** several are very recent / arXiv-only / "Unknown Journal" —
expect some to come back `verified:false` (flag, don't drop; Chris decides). Adopt-
cite trio for §1.7 (Zep, H-MEM, Pavlović + Collins & Loftus 1975) added only if the
draft keeps decay / multi-resolution / spreading-activation as named comparison arms.
