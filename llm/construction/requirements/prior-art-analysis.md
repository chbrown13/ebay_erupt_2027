# Prior-Art & Problem Validation — eRUPT Agentic-KG Proposal

> Deliverable for spec §4C (novelty gate). Produced 2026-06-25 by the
> `erupt-novelty-gate` ultracode workflow: 4 parallel Consensus searches +
> adversarial synthesis. **Verdict: `partial-overlap` → reposition.**
> Source run: `wf_e68c4468-0b6`.

## Verdict

**`partial-overlap`.** It **is the right problem** (the enterprise code-review
bottleneck and audit/reproducibility needs are real, valued by eBay, and unsolved
at the open-ended-LLM-generation scope) — **but the broad framing is not novel.**
Four independent facets converged: "KG over a codebase → agentic
retrieval-conditioned generation" is a 2024–2025 mini-trend with a SWE-bench SOTA
exemplar and an **architectural near-twin that already prints our exact
retrieval/generation/verification agent split.** We must cede the core and stake
the claim narrowly.

## Closest competing work (the threats)

| Work | Year | Why it's dangerous | What it still misses |
|------|------|--------------------|----------------------|
| **GRACG** — Graph Retrieval Augmented Code Generation (Fedorov et al.) | 2025 | **Architectural twin.** Code KG + graph retrieval to ground LLM generation, *explicitly* the same retrieval/generation/verification multi-agent split we pitch. | Static structural snapshot (no git history/PRs/reviews); no provenance, determinism, or convention pipeline; no enterprise case study. |
| **SemanticForge** (Zhang et al.) | 2025 | Closest on **"deterministic + auditable."** Per-repo KG + SMT-guided beam search → code *provably* satisfies repo semantics; incremental graph state ≈ "same KG state → same output." | KG is current code, not history; no provenance trace; no agent split; no convention gate. |
| **Janke & Mader** — Graph mining of code-change patterns from VCS commits | 2022 | Pre-empts our **"graph over git history with provenance"** angle: context-preserving graph from commits + frequent-subgraph mining → interpretable, commit-traceable patterns. | Stops at pattern *discovery* (no generation, no agents, no standing KG; cross-project not single-org). |
| **PYEVOLVE** (Dilhara, Ketkar, Sannidhi, Dig) | 2023 | Pre-empts **"deterministic, history-grounded automated change":** mines change patterns from history, transplants them (97% precision, 90% dev acceptance). | Deterministic *AST rewriting of narrow syntactic patterns* — cannot author a novel ViewItem "signal"; no KG/agents/convention pipeline. |
| **GraphCodeAgent** (Li et al.) | 2025 | Confirms agentic multi-hop retrieval over a repo graph → repo-level generation is established (beats SOTA RACG baselines). | No history/provenance/determinism/auditability/convention validation. |
| **RepoGraph** (Ouyang et al.) | 2024 | Most-validated (SWE-bench SOTA, ~85 cites): code graphs help agentic SWE — adjacent to our case study. | Static structure; navigation not provenance; no determinism/audit/convention gate. |
| **Athale & Vaddina** — KG-Based Repository-Level Code Generation | 2025 | Closest in **name & intent** ("KG over codebase → retrieve → consistent generation"); appeared in 3 of 4 facets. | Static structure/dependency KG; no history, agents, determinism, provenance, or convention pipeline. |
| **Tao et al.** — RACG survey (repo-level focus) | 2025 | Establishes graph-retrieval substrates + agent architectures as recognized, crowded threads; raises the bar. | (Survey.) Flags reliability as open; surfaces no history-provenance/determinism/convention system. |

## Gap statement (what is genuinely new)

No single retrieved system combines all of our load-bearing elements, so our
novelty is **narrow and conjunctive, not foundational.** The KG-grounded agentic
code-generation core is fully anticipated (GRACG, GraphCodeAgent, RepoGraph,
Athale & Vaddina) — **do not claim it.** Constraint-driven "deterministic +
auditable" generation over a code KG already exists (SemanticForge). Provenance-
aware graphs mined from git history already exist (Janke & Mader), as does
deterministic history-grounded change automation (PYEVOLVE). What no retrieved
work does is the **specific marriage**: a persistent, provenance-aware KG over a
single enterprise's *full version-control history* (commits + PRs + code-review
discussions, not an AST snapshot) as the retrieval substrate for multi-agent LLM
generation, where (a) each change traces to specific historical artifacts/
decisions, (b) reproducibility is keyed to a **frozen KG provenance state** (not
SMT constraint-correctness), and (c) a validation pipeline checks agent-generated
PRs against **KG-encoded team conventions** to attack the review bottleneck. That
combination — applied to *open-ended* LLM feature generation in an enterprise
setting — is the only defensible novelty, and it is a harder, partly unproven
claim precisely because the works that achieve determinism (PYEVOLVE) and
constraint-auditability (SemanticForge) do so by *not* attempting open-ended
generation.

## Repositioning plan (6 moves)

1. **Cede the core explicitly.** State up front that KG-grounded agentic
   repo-level codegen with retrieval/generation/validation roles is established
   (cite GRACG, GraphCodeAgent, RepoGraph, Athale & Vaddina); we **extend**, not
   invent it. Pre-empts the GRACG kill-shot.
2. **Make HISTORY the substrate, not structure.** Every figure, the schema, and
   the case study must foreground commit/PR/review nodes & edges. If any artifact
   reads as "AST of current code," we collapse into Athale/SemanticForge. Cite
   Janke & Mader and PYEVOLVE as proof the history-mining premise is sound.
3. **Redefine "deterministic" precisely** as **provenance-reproducibility**
   (frozen KG provenance state → same retrieval set → same conditioned output,
   with a recorded trace). Contrast with SemanticForge's constraint-correctness
   and PYEVOLVE's rule-rewrite determinism. Acknowledge LLM sampling
   nondeterminism and specify the mechanism (fixed retrieval + temperature-0 +
   pinned model + provenance hash) or expect a challenge.
4. **Elevate the convention-validation gate to a co-equal contribution** with its
   own evaluation — it's the element least covered by *any* retrieved work.
5. **Frame the eBay ViewItem "signal" study** as the open-ended-feature stress
   test that mining/transplant systems (PYEVOLVE) provably cannot author — our
   strongest narrative wedge. Label it **practical relevance, not research
   novelty.**
6. **Add one missing search:** software-supply-chain / build-provenance (e.g.,
   **SLSA**) for AI-generated code — the neighbor most likely to pre-empt the
   provenance/audit claim. Consensus's codegen-tilted results did not surface it;
   worth one targeted pass before a reviewer raises it.

## Recommended citations (real, Consensus-surfaced — become reference candidates)

All eight closest-work papers above are high-impact "distinguish-from" cites.
Priority "must-distinguish-from": **GRACG** (identical agent split),
**SemanticForge** (determinism analog), **Janke & Mader** + **PYEVOLVE**
(history/determinism premise), **RepoGraph** (validated baseline),
**Athale & Vaddina** (canonical KG+codegen), **GraphCodeAgent** (agentic loop),
**Tao et al.** (landscape/positioning). URLs recorded in the source run /
references store when sourced.

## Problem-centric re-analysis (2026-06-26)

The first gate compared on **mechanism** (KG + retrieval + agents). But
mechanism-similarity ≠ problem-similarity. Re-examined by the **problem each work
targets**:

| Cluster | Works | The problem *they* solve | Their yardstick |
|---------|-------|--------------------------|-----------------|
| **Codegen accuracy** | GRACG, GraphCodeAgent, RepoGraph, Athale & Vaddina, SemanticForge | produce more correct / consistent code at repo level | Pass@1, SWE-bench, EvoCodeBench |
| **Mechanical-change automation** | Janke & Mader, PYEVOLVE, **PyCraft** | apply known, narrow, syntactic transformations at scale | precision/recall, PR acceptance |

**Our problem is neither.** It is enterprise developer **velocity** on recurring
tasks (weeks→hours), **organizational memory**, and the **AI-PR review/trust
bottleneck** — grounded in one org's own history. Yardstick = developer-time per
task, PR acceptance / review burden, convention conformance.

### Problem-occupancy search (second Consensus pass)

Searched for work targeting OUR problem (not the mechanism). The problem **is**
being actively pursued — which for an eRUPT grant is *good* (it validates
relevance and value) — but no one occupies our specific synthesis. Closest:

- **PyCraft** (Dilhara et al., 2024) — LLM + Transformation-by-Example automates
  recurring code-change patterns (CPATs); 83% of submitted PRs merged into
  projects like Microsoft/DeepSpeed. Closest on "automate recurring changes,"
  now LLM-augmented — but still semantically-equivalent *transformations*, not
  open-ended feature authoring; no org-history KG; no convention governance.
- **ICR — Intelligent Code Reviewer** (Nimraka et al., 2025) — agentic multi-LLM
  PR review (bugs/security/perf) with GNN duplication detection, dependency-impact
  analysis, and **PR validation against custom company rules**. Closest on the
  review-bottleneck + convention-validation pillar — but it *reviews* PRs; it
  doesn't generate from history or build an org code-pattern KG.
- **Knowledge Activation / AKUs** (Bakal, 2026) — closest on PROBLEM: enterprise
  institutional knowledge as a composable knowledge graph agents traverse, to
  compress onboarding, cut cross-team friction, and reduce the "senior-engineer
  tax." **Yahoo deployment: 2.6 hrs/week saved, NPS +35.** But its substrate is
  *curated* knowledge units (architecture/deploy/compliance/playbooks), not
  code-history-mined patterns for deterministic generation, and it has no
  PR-convention-validation gate.

### Refined verdict

The **problem is validated and valuable** (industry is investing, with measured
DX gains — notably the Yahoo/AKU result), the **mechanism is crowded**, and the
**specific contribution remains open**: a provenance-aware KG over the org's *own*
version-control history (commits/PRs/reviews) → deterministic, traceable
generation of recurring changes → validated against KG-encoded conventions.
Honest framing = **problem-led**, not a defensive novelty stack. This is stronger
and more defensible than the first gate's "cede everything / claim a narrow
feature conjunction" advice.

**New must-cite (problem-side):** PyCraft (Dilhara 2024), ICR (Nimraka 2025),
Knowledge Activation/AKUs (Bakal 2026).

## Follow-up findings (2026-06-26) — both resolved

### AKUs (Bakal 2026, arXiv:2603.14805) — full read
Closest work on PROBLEM ("institutional impedance mismatch" + the
"institutional knowledge tax" on senior engineers; a composable knowledge graph
agents traverse; Yahoo deployment: 67 engineers, **2.6 hrs/week saved, NPS +35**).
Three **decisive** differences from ours, confirmed in the full text:
1. **Substrate is human-authored / curated** ("codify the top five to ten
   skills"), **NOT mined from version-control history.** Ours auto-mines
   git/PR/review history. *(The core differentiator.)*
2. **Does NOT generate code** — delivers "action-ready specifications" / guidance
   to agents and engineers. Ours generates the recurring code change.
3. **"Validators" are deterministic scripts inside a skill** (execution-time),
   **not PR-level validation against historical team conventions / CI.**
- **Wedge:** AKUs explicitly lists "plugin **staleness** detection" as unresolved
  future work — a history-mined, continuously-updated KG directly attacks the
  staleness that curated knowledge suffers. Strong positioning point.
- **Use:** cite as motivation/validation of the problem (the knowledge-tax + the
  Yahoo numbers prove eBay-relevance and value) and distinguish on
  substrate + generation + PR-convention gate.

### SLSA / build-provenance — does NOT pre-empt our provenance claim
Supply-chain frameworks (SLSA, SBOM, in-toto, Sigstore) provide **build-integrity
provenance for security**; a 2025 agentic-supply-chain paper notes they "mainly
provide provenance and traceability but cannot actively identify or remove
vulnerabilities." That is a **different layer** from ours: our provenance =
traceability of a generated change to the **historical patterns/decisions** that
produced it (*generation* provenance), not cryptographic *build* attestation.
They **compose** rather than compete (a generated PR could carry both). No
repositioning needed; one clarifying sentence pre-empts the objection.

### Net effect on the verdict
The problem-led framing holds and is now well-defended on every flagged neighbor.
Closest-on-problem (AKUs) differs decisively on substrate + generation + gate;
closest-on-mechanism (GRACG/SemanticForge) solves codegen-accuracy, not our
problem; the provenance/audit claim is a different layer from SLSA. **Defensible
contribution = auto-mined code-history provenance KG → deterministic, traceable
generation of recurring changes → PR validation against KG-encoded conventions.**

## Deeper re-search (retargeted queries, 2026-06-26)

> Note: the Consensus connector remained capped at top-3 results per query
> (website login did not propagate to the MCP session), so ranks 4–20 are unseen;
> "View all 20" browser links exist per query. Retargeted queries still surfaced
> new top-ranked neighbors. **Verdict unchanged (partial-overlap, problem-led);**
> two important new must-cites added on the traceability/determinism pillar.

- **Embedding Traceability in LLM Code Generation** (Wang et al., 2025, FSE) —
  **closest neighbor on our auditability/traceability pillar.** Makes traceability
  a first-class objective in LLM codegen (structured requirement prompting,
  metadata-aware fine-tuning, retrieval-augmented validation) for "audit-ready
  code generation," explicitly naming LLMs' non-determinism ("divergent outputs
  from identical prompts"). **Distinguish:** it traces to *requirements*, not to
  *historical code patterns/decisions mined from the org's VCS*. Must-cite.
- **AI-Generated Code Is Not Reproducible (Yet)** (Vangala et al., 2025) —
  empirical evidence that LLM coding agents (Claude Code, Codex, Gemini) produce
  non-reproducible code (68.3% run out-of-box; 13.5× hidden-dependency expansion).
  **Strong motivation** that AI-codegen reproducibility is a real open problem —
  but its "reproducibility" = dependency/execution, a *different sense* than our
  provenance-reproducibility (same KG state → same output). Cite as motivation
  AND to disambiguate our determinism claim.
- **CCT5: A Code-Change-Oriented Pre-trained Model** (Lin et al., 2023, FSE,
  61 cites) — models code changes from 1.5M commit/message pairs; notes
  code-change tasks are ~**70% of development expenditure**. Cite for the
  cost-of-recurring-change motivation and as code-change-modeling prior art (no
  KG / agentic generation+validation loop / determinism).
- Mechanism re-run reconfirmed Athale & Vaddina and GRACG as the closest; nothing
  nearer surfaced in top-3.

**Refined must-cite additions:** Wang 2025 (traceability), Vangala 2025
(reproducibility motivation), CCT5 (code-change cost). The determinism claim now
needs **two explicit contrasts** in the proposal: vs. Wang's requirement-traceability
and vs. Vangala's dependency-reproducibility.
