# Project Brief

> Foundation document. Changes rarely. Read this first after a context reset.

## Overview

Write and submit a research-collaboration **grant proposal** to eBay's eRUPT
program for a project titled **"Agentic Knowledge Graphs over Code History for
Enterprise Software Automation."** The proposed research mines a provenance-aware
knowledge graph (KG) from eBay's *own version-control history* — git commits, PRs,
code reviews (plus AST structure) — and uses that single substrate both to
*generate* recurring code changes consistent with past practice and to *validate*
the resulting PRs against the team's historical conventions. Generation is
auditable and reproducible from a fixed KG state — but **determinism is a
supporting property, not the headline** (the headline is the history-mined
substrate; see `productContext.md` for the framing and `prior-art-analysis.md`
for why).

This repo produces the **proposal artifact**, not the system itself. The system
is what the grant would fund.

## Objectives (of the proposal)

- Make the case that mining historical code patterns into a queryable KG can make
  recurring eBay code tasks (e.g., adding a signal to a ViewItem page)
  deterministically automatable.
- Map cleanly onto eBay eRUPT's required 7-section structure (see
  `llm/construction/requirements/cfp-analysis.md`).
- Demonstrate fit with eBay's real infrastructure (Compass KG) and the team's
  prior work: FOSE 2026 (cited [1]) and provenance-aware agentic-KG work (used as
  **uncited background** — the DOE Genesis proposal is under submission at another
  venue and must **not** be cited, per PR #1 review).

## Engagement Structure

| Role | Person |
|------|--------|
| PI | Dr. Chris Brown (Virginia Tech) |
| GRA / lead researcher | Jason Cusati (VT PhD candidate) |
| eBay Co-Investigator | Ramesh Periyathambi |
| eBay VP/Head | TBD — needs Ramesh's input (placeholder in draft) |
| Grant amount | **$120,000** (one-year grant); top of eRUPT range |

## Target Venue

- **Name**: eBay eRUPT Academic Research Grants (2026/27 cycle)
- **Type**: Company-sponsored research grant (1-year)
- **Submission deadline**: **September 21, 2026** → `erupt@ebay.com`
- **Page limit**: Not specified; template runs ~2–3 pages of content
- **Format**: `files/eRUPT 2026_27 Template for Academic Research Collaboration Proposals.docx`
- **IP terms**: eBay expects royalty-free license rights at minimum; permissive
  open-source possible depending on the work.

## Research Questions (proposed)

1. Can historical code patterns be mined from a production codebase and
   represented as a queryable knowledge graph?
2. Can an agentic workflow use that history-mined KG as the **unified substrate**
   for both generation (conditioned on provenance-tagged patterns, not LLM priors)
   and convention-validation of the resulting PR?
3. Can the convention-validation gate check agent-generated PRs against
   KG-encoded *historical team conventions* — supporting, not replacing, reviewers
   — to ease the human code-review bottleneck?

## Scope

### In Scope
- eBay enterprise Java codebase as the target domain
- Code-pattern mining (AST + git/PR history) into a KG
- Agentic orchestration (ranking / generation / validation agents)
- ViewItem signals as the scoped case-study pattern

### Out of Scope
- Scientific-software / HPC domains (that's the DOE Genesis sibling project)
- General-purpose knowledge accumulation untethered from code generation
- Building production infrastructure within the proposal itself (this repo is the
  proposal; the system is the funded deliverable)

## Success Criteria

- [x] Proposal answers all 7 eRUPT sections in order
- [~] Engagement table — $120K set; **VP/Head name still a placeholder** (Ramesh)
- [x] Claims supported by **§4A-verified** references (14: 13 verified, 1 flagged)
- [x] Compiles cleanly from `proposal/main.tex`
- [x] Reviewed via PR #1 + #2 (Chris); **Ramesh review pending** (Chris emailing)
- [ ] Converted to the eBay **.docx** template
- [ ] Submitted before September 21, 2026

See `productContext.md` for *why*, `systemPatterns.md` for *how the proposed
system works*, `activeContext.md` for *current state*, `progress.md` for *status*.
