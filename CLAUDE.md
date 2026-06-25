# Agentic Knowledge Graphs for Code Generation

## Project Overview

This project will explore using agentic knowledge graphs for supporting agentic software development at eBay. The goal is to have a knowledge graph of prior issues, PRs, commits, bug reports, etc. and see if knowledge graphs can support agents in deterministically generating solutions for future bug reports, issues, and features.

## Documentation System

This project uses a **memory-bank** documentation approach:

- `llm/memory-bank/` — Living documentation (project context, decisions, progress)
- `llm/construction/` — Design-first development workspace (designs, requirements, sprints)
- `.claude/agents/` — Specialized agent configurations

## Quick Start

1. Read `llm/memory-bank/activeContext.md` for current status
2. Read `llm/memory-bank/projectbrief.md` for core objectives
3. Read `llm/memory-bank/progress.md` for task tracking
4. Check `llm/construction/` for active design work

## Paper Type

<!-- Uncomment the paper type you are writing -->
type: proposal
<!-- type: research-paper -->
<!-- type: position-paper -->

## Key Deadlines

| Date | Milestone |
|------|-----------|
| September 21 | eRUPT Ebay deadline |
| July 8 | Send draft to Ramesh at Ebay |
| June 22 | Send proposal draft to Jason |

## Submission Requirements

- **Venue/Target**: eBay
- **Page Limit**: Not specified
- **Format**: custom (see files/eRUPT 2026_27 Template for Academic Research Collaboration Proposals.docx)
- **Submission Portal**: erupt@ebay.com
- **Additional Requirements**: All proposals will be considered, provided they are relevant to eBay and have the potential to advance the state of the art. eBay is interested in the practical application of the results and expects to, at a minimum, have royalty free license rights to the resulting project IP without additional licensing costs. Open sourcing results under a permissive license may be an option as well depending on the nature of the research.

## Key Locations

| Path | Description |
|------|-------------|
| `files/` | Reference materials, CFP docs, venue guidelines |
| `llm/memory-bank/` | Living project documentation |
| `llm/construction/` | Design workspace |
| `.claude/agents/` | Agent configurations |
| call for papers | see ./files/2027 eRUPT Academic Research Grants - External (1).pdf |
| prior ebay eRUPT example | see ./files/eRupt_exampple.docx |
| approach background | see ./files/cusati-brown-fose2026-preprint.pdf, ./files/doe-genesis.tex, ./files/doe-abstract.pdf, and ./files/amazon.pdf |

## Agent Reference

| Agent | Purpose |
|-------|---------|
| `latex-agent` | LaTeX compilation, formatting, bibliography management |
| `proposal-agent` | Research proposal / CFP workflow (design → validate) |
| `paper-agent` | Research paper workflow (outline → draft → revise) |
| `position-paper-agent` | Position/vision paper workflow |
| `memory-agent` | Memory-bank documentation maintenance |
| `review-agent` | Quality gate: citations, compilation, content checks |

Choose the agent matching your paper type. The `latex-agent` and `review-agent` are used by all paper types.
