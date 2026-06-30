# Project Brief

> Foundation document. Changes rarely. Read this first after a context reset.

## Overview

Write and submit a research-collaboration **grant proposal** to eBay's eRUPT
program for a project titled **"Agentic Knowledge Graphs for Deterministic Code
Generation."** The proposed research builds an agentic knowledge graph (KG) over
eBay's historical code — git history, PRs, code reviews, dependency structure —
so that an AI agent can generate code for recurring patterns *deterministically*:
same task + same KG state → same output.

This repo produces the **proposal artifact**, not the system itself. The system
is what the grant would fund.

## Objectives (of the proposal)

- Make the case that mining historical code patterns into a queryable KG can make
  recurring eBay code tasks (e.g., adding a signal to a ViewItem page)
  deterministically automatable.
- Map cleanly onto eBay eRUPT's required 7-section structure (see
  `llm/construction/requirements/cfp-analysis.md`).
- Demonstrate fit with eBay's real infrastructure (Compass KG) and our prior work
  (DOE Genesis PA-AKG, FOSE 2026).

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
2. Can an agentic workflow use that KG as structured context to generate code
   *deterministically* (vs. relying on LLM priors alone)?
3. Can an automated validation pipeline check agent-generated PRs against
   KG-encoded conventions, reducing the human code-review bottleneck?

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

- [ ] Proposal answers all 7 eRUPT sections in order
- [ ] Engagement table complete (VP name, grant amount filled in)
- [ ] Claims supported by references; reference list fleshed out (currently thin)
- [ ] Compiles cleanly from `proposal/main.tex`
- [ ] Reviewed by Jason (target was June 22) and Ramesh (target ~July 8)
- [ ] Submitted before September 21, 2026

See `productContext.md` for *why*, `systemPatterns.md` for *how the proposed
system works*, `activeContext.md` for *current state*, `progress.md` for *status*.
