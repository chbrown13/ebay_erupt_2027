# Product Context

> The *why*. Changes occasionally. Read after `projectbrief.md`.
> **v2 (2026-07-07):** scaled from a single ViewItem page to the whole
> multi-repository codebase; novelty relocated to the empirical comparison.

## Problem Statement

At eBay, shipping a feature rarely touches a single codebase. A *codebase* is one
repository; a feature is what spans several of them — **typically 5+, per Ramesh**.
On a large, long-lived, multi-repository codebase, the dominant cost is
*understanding*: a developer (or a coding agent) must learn each repository's APIs,
conventions, dependencies, and history before making a change. Three pains follow:

1. **Onboarding** — bringing a developer or agent up to speed on an unfamiliar
   repository is repeated from scratch every time.
2. **Cross-repo feature velocity** — a single feature can take a year or more
   (incl. A/B testing) and spans many services owned by many teams.
3. **Review bottleneck** — every change, and increasingly every AI-generated
   change, must still be read and approved by a human.

The deeper problem: a multi-repo codebase holds enormous *historical* knowledge
(which files/services change together, which APIs are called, what review feedback
recurs) scattered across commits, PRs, JIRA work items, code patterns, and external
resources — inaccessible to an agent, which instead generates from internet-scale
priors that violate team conventions.

## Proposed Approach

Mine a **provenance-aware agentic knowledge graph** from eBay's *own*
multi-repository version-control history, and — the contribution — **compare,
empirically, how an agent should retrieve from it**. Build the substrate once as a
*family of graphs* (Repo / JIRA / Memory-Bank); then run a head-to-head of three
retrieval strategies (graph query vs. similarity/RAG vs. spreading activation) to
find which makes an agent most efficient at multi-repo understanding. On the best
strategy, the agent *synthesizes* cross-repo features and a gate *validates* the
resulting PRs against KG-encoded conventions.

## Key Concepts (v2 terminology)

- **Codebase = one repository;** a **feature** spans several (5+).
- **Family of graphs** — Repo Graph (services/repos), JIRA Graph (work items →
  commits/PRs → external resources), Memory-Bank Graph (per-repo living docs).
- **Retrieval strategies (the experiment)** — (a) graph query, (b) similarity/RAG,
  (c) **spreading activation** (activation diffuses across edges; Collins & Loftus
  1975; Pavlović 2025). Time-weighted (decay) edges + multi-resolution nodes.
- **ViewItem / signal / signal handler** — *demoted to a one-line micro-example*
  (still eBay-unverified terminology; v2 barely leans on it).

## Key Differentiators (v2)

> **Novelty gate (v2, `v2-prior-art-analysis.md`): partial-overlap.** Every
> *mechanism* (graph-of-graphs, memory-bank traversal, decay/multi-resolution/
> spreading-activation) is crowded 2025–26 prior art — do **not** claim them.

- **The empirical comparison IS the contribution** — nobody has run a head-to-head
  of retrieval strategies for multi-repo coding-agent understanding. Sidesteps
  every mechanism-novelty fight.
- **Cross-repo feature *synthesis*** on the org-history substrate — the sharpest
  stake-able new claim (distinct from CCCE's *maintenance* and Learning to Commit's
  *single-repo* mining).
- **History-mined, cross-repository substrate** — self-updating, provenance-tagged;
  extends eBay's Compass with code-level pattern knowledge tickets don't capture.
- **Determinism: dropped entirely** in v2 (was already demoted in v1) — it was the
  most crowded claim; the story is now the substrate + the comparison.

## Value Propositions (the eRUPT "Impact" pitch)

1. **Onboarding** — query a repo's conventions/owners/rationale ("what changed and
   why" [Yates]) instead of shadowing seniors.
2. **Cross-repo feature velocity** — scaffold changes that correctly span the
   services a feature touches.
3. **Review unblocking** — convention-grounded conformance checks flag only genuine
   anomalies (support, not replacement); DeputyDev-style 31.8% review-cycle lever.

## Target Audience

- **Proposal readers**: eBay eRUPT reviewers (relevance to eBay, advancing state of
  the art, practical application).
- **Eventual system users**: eBay developers, engineering managers, SE researchers.
