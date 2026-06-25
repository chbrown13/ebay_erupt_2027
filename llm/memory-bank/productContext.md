# Product Context

> The *why*. Changes occasionally. Read after `projectbrief.md`.

## Problem Statement

At eBay, recurring code tasks repeat hundreds of times a year and each one is
slow. Adding a new **signal** to a **ViewItem page** (eBay's product-detail page),
or wiring up an A/B-test variant, reportedly takes a developer **2–4 weeks every
time** — because the relevant files, APIs, and undocumented team conventions have
to be rediscovered from scratch on each iteration. This silently drains
engineering velocity at scale.

The deeper problem: a codebase that has existed for years holds enormous
historical knowledge (which files change together, which APIs are called, what
review feedback recurs), but that knowledge isn't captured in a form an AI agent
can use. Today's agents generate code from LLM priors, not from the
organization's own history — so output is non-deterministic and untrustworthy for
production.

## Proposed Approach

Build a **provenance-aware agentic knowledge graph** over eBay's code history.
Agents *retrieve* relevant prior patterns from the KG and *write* validated
outcomes back to it. Because generation is conditioned on a concrete KG state
rather than model priors, the same request against the same KG yields the same
code — deterministic and auditable, with every recommendation traceable to a
historical pattern.

## Key Concepts (proposal terminology)

- **ViewItem page** — eBay's high-traffic single-listing product page. Constantly
  modified, heavily instrumented → a good source of recurring patterns.
- **Signal** — a tracked behavioral/instrumentation event emitted from the page
  (view events, experiment exposures, feature-flag fires) that feeds
  recommendations, ranking, experimentation, analytics.
- **Signal handler** — the code component that receives, transforms, and routes a
  signal to downstream services (api gateway, metrics client, experimentation
  platform). In the KG it appears as a recurring sub-graph:
  `ApiGateway`/`SignalHandler`/`MetricsClient` nodes with typed edges
  (`imports`, `implements`, `dependsOn`).

> Caveat: these are illustrative terms in the proposal, not yet verified against
> eBay's actual internal architecture. Confirm exact terminology with Ramesh to
> strengthen credibility.

## Key Differentiators

- **Provenance-aware** KG: outputs trace back to specific historical patterns.
- **Determinism**: same KG state → same generated code (vs. RAG / vanilla LLM).
- **Practical, eBay-grounded**: extends eBay's existing Compass KG with
  code-level pattern knowledge that tickets don't capture.

## Value Propositions (the eRUPT "Impact" pitch)

1. **Velocity** — collapse recurring tasks from weeks to hours.
2. **Organizational memory** — new hires, offshore teams, internal transfers query
   conventions and dependency ownership instead of shadowing seniors for weeks.
3. **Code-review unblocking** — automated conformance checking flags only genuine
   anomalies in agent-generated PRs, addressing eBay's review bottleneck.

## Target Audience

- **Proposal readers**: eBay eRUPT reviewers (judge on relevance to eBay, advancing
  state of the art, practical application).
- **Eventual system users**: eBay software developers, engineering managers, and
  SE researchers.
