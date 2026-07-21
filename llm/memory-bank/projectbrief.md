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

- **(v2)** Make the case that a coding agent grounded in a KG mined from the org's
  **multi-repository** version-control history can be made efficient at
  understanding a large codebase — and **determine empirically which retrieval
  strategy does it best** (graph query vs. similarity/RAG vs. spreading
  activation). *codebase = one repository; an eBay feature spans 5+.*
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
| eBay VP/Head | **Rami El-Charif** (filled by Chris, 2026-07-07) |
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

1. Can a **multi-repository** code history (commits, GitHub PRs, JIRA work items,
   code patterns, external resources) be mined into a **family of graphs** (Repo /
   JIRA / Memory-Bank) a coding agent can traverse?
2. **Which retrieval strategy over that history — graph query vs. similarity/RAG
   vs. spreading activation — makes the agent most efficient at multi-repo
   understanding?** (The empirical comparison is the headline contribution.)
3. Can the agent **synthesize a feature spanning several repositories** from mined
   historical patterns, and can a validation gate check the resulting PRs against
   KG-encoded *cross-repo* conventions — supporting, not replacing, reviewers?

## Scope

### In Scope (v2)
- eBay enterprise Java codebase, **multi-repository** (case-study bound ~10 repos)
- History mining (commits, PRs, JIRA work items, code patterns, external refs)
  into a **family of graphs** (Repo / JIRA / Memory-Bank), time-weighted + multi-res
- **Empirical comparison** of 3 retrieval strategies (the contribution)
- Cross-repo feature synthesis + cross-repo convention-validation gate

### Out of Scope
- Scientific-software / HPC domains (that's the DOE Genesis sibling project)
- General-purpose knowledge accumulation untethered from code generation
- Building production infrastructure within the proposal itself (this repo is the
  proposal; the system is the funded deliverable)

## Success Criteria

- [x] Proposal answers all 7 eRUPT sections in order (v1 + v2)
- [x] **v2 drafted** (`proposal/v2-main.tex`), scaled to multi-repo; compiles clean
- [x] Claims supported by **§4A-verified** references (22: 21 verified, 1 flagged)
- [x] **v2 novelty gate** run → `partial-overlap`; framing repositioned accordingly
- [x] **PR #8 merged** (Chris); CI green + APPROVED
- [x] **Website live** → https://chbrown13.github.io/ebay_erupt_2027/
- [x] Engagement table — $120K set; **VP/Head = Rami El-Charif** (Chris, 2026-07-07)
- [x] Converted to the eBay **.docx** template (`proposal/eRUPT-proposal-v2.docx`)
- [x] **Review feedback incorporated** (2 passes) → PR #10, CI green (awaiting merge)
- [ ] Confirm lab name "Code World No Blanket" + time/effort costs (human)
- [ ] Submitted before September 21, 2026

See `productContext.md` for *why*, `systemPatterns.md` for *how the proposed
system works*, `activeContext.md` for *current state*, `progress.md` for *status*.
