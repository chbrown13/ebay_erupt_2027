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

## Open follow-up
- [ ] Targeted Consensus pass on SLSA / build-provenance for AI-generated code
      (move 6) to confirm the provenance/audit gap holds.
