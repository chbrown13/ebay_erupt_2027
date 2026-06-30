# Specification: eRUPT Proposal — References Section

> Produced via `constellize-design:specification`. Scope = the **References**
> section of `proposal/main.tex` and every in-text citation that feeds it.
> This is a *spec for the deliverable*, not the references themselves.
> Status: Draft · 2026-06-25

## 0. Context & Problem

The proposal currently exposes **two** reference entries (`[1]` FOSE 2026,
`[2]` VersiCode) while the prose makes several citable claims that have **no
backing reference** (Compass, DOE Genesis/PA-AKG as a distinct project) or
**reuse `[1]` ambiguously** (FOSE and DOE Genesis both point to `[1]`). The
"Previous Work" and "Methodologies" sections therefore read as under-evidenced
for an eRUPT panel judging *advancement of the state of the art*.

Goal of the references work: every citable claim resolves to a **real,
verifiable** reference; the list is complete, consistent, and template-legal —
without inventing sources or leaking eBay-internal detail.

---

## 1. Functional Requirements

### 1.1 Coverage — claims that MUST have a reference
- **FR-001 (Must):** The FOSE 2026 position paper must be a distinct entry,
  cited where "structured knowledge accumulation" / intellectual-foundation
  claims appear. *Source: `files/cusati-brown-fose2026-preprint.pdf` (real).*
- **FR-002 (Must):** The DOE **Genesis / PA-AKG** project must be cited as a
  **separate** reference from FOSE (it is currently conflated with `[1]`).
  *Source: `files/doe-genesis.tex`, `files/doe-abstract.pdf` — derive an
  accurate project/grant citation.*
- **FR-003 (Must):** **VersiCode** must remain, cited at the version-aware /
  API-evolution claim. *Source: arXiv:2406.07411 (verify id + authors).*
- **FR-004 (Should):** **Compass** (eBay enterprise KG) — if no public citation
  exists, represent it honestly as eBay-internal (e.g., "eBay internal system;
  personal communication, R. Periyathambi") rather than a fabricated paper.
  Flag for Ramesh to confirm the correct public reference, if any.

### 1.2 Coverage — methodology claims that SHOULD gain support
- **FR-005 (Should):** AST-based code structure extraction — cite a foundational
  source for AST/code-representation mining.
- **FR-006 (Should):** Frequent-subgraph / pattern mining over code graphs —
  cite a graph-mining or code-KG reference.
- **FR-007 (Should):** Agentic / multi-agent LLM code generation (ranking,
  generation, validation roles) — cite ≥1 representative agentic-coding work.
- ~~FR-008 (Nice): RAG baseline citation~~ — **Dropped 2026-06-25** (keep the list
  lean for a 2–3 page proposal; revisit only if the eval section explicitly names
  RAG as a baseline — it currently does not).
- ~~FR-009 (Nice): AI-PR / code-review-bottleneck citation~~ — **Dropped
  2026-06-25** (optional, low leverage).

### 1.3 Mechanics
- **FR-010 (Must):** Every in-text marker `[n]` resolves to exactly one entry;
  every entry is cited at least once (no orphans, no dangling markers).
- **FR-011 (Must):** Renumber sequentially in order of first appearance after
  entries are added/split (FOSE/DOE split changes the numbering).
- **FR-012 (Must):** Mirror every entry into
  `llm/construction/requirements/citation-matrix.md` with a `Verified` flag.
- **FR-013 (Should):** Keep the entry format consistent with the current style
  (author, "title," venue/arXiv, year) unless we migrate to BibTeX.

### 1.4 Reference store
- **FR-014 (Must):** All references live in a **single canonical machine-readable
  store**, `llm/construction/requirements/references.json`. Each entry carries:
  `id`, `marker`, bibliographic fields (`authors`, `title`, `venue`, `year`,
  `url`/`arxiv`/`doi`), `source` (local file or public locator), `supportsClaims`,
  and a `verification` block (see §4A). `proposal/main.tex` and
  `citation-matrix.md` are **generated/derived views** of this store and must
  stay in sync with it.
- **FR-015 (Must):** No entry may carry fabricated bibliographic metadata. A
  planned-but-unwritten reference is recorded under `planned` (role + candidate
  source only), never as a fake complete entry.

---

## 1A. Reference Impact Ranking (inclusion scoring)

The final list is **budget-limited** (~5–8 entries, NFR-002), so inclusion of the
*Should* candidates is decided by **impact score**, not guesswork. Score each
candidate on four factors (1–3 each; max 12):

| Factor | 3 | 2 | 1 |
|--------|---|---|---|
| **Claim criticality** | backs a Must claim | backs a Should claim | backs a Nice claim |
| **Source strength** | peer-reviewed, strong venue / well-cited | solid peer-reviewed or widely-cited preprint | low-cited / preprint / non-archival |
| **Novelty positioning** | defines the gap / state-of-the-art we advance | contextualizes the approach | tangential background |
| **Reviewer salience** | an eRUPT reviewer would expect this cite | helpful, not expected | unlikely to be missed |

**Tiers → inclusion:**
- **A (10–12):** Must include.
- **B (7–9):** Include by rank until the ~5–8 budget is full.
- **C (4–6):** Optional; only with spare space and clear value.
- **D (≤3):** Exclude.

**Rules:**
- Must-claim references (FR-001–003) auto-qualify regardless of score — coverage
  requires them. The ranking governs the *Should* candidates competing for the
  remaining slots.
- **FR-016 (Must):** Every candidate gets an impact score recorded in its store
  entry (`impact` block: the four sub-scores + total + tier). Final inclusion of
  Should-tier refs follows rank within the NFR-002 budget. **Excluded candidates
  are logged** (no silent drops) with their score and the reason.

---

## 2. Non-Functional Requirements

- **NFR-001 Accuracy / no hallucination (Must):** No fabricated citations. Every
  reference must pass the §4A verification protocol before it is allowed to ship
  with `verified: true`. Any reference whose metadata cannot be confirmed against
  `files/` or a checkable public source stays `verified: false` and is flagged,
  not asserted.
- **NFR-002 Compactness (Must):** eRUPT proposals are ~2–3 pages; target a
  **focused list (~5–8 entries)**. Prefer the highest-leverage citations over
  breadth. Rationale: padding the list hurts a short-form proposal.
- **NFR-003 Template legality (Must):** References render cleanly in the LaTeX
  draft *and* survive conversion to the required eBay **.docx** template.
- **NFR-004 Confidentiality (Must):** No eBay-internal/proprietary detail
  encoded in citations (esp. Compass). Honor eRUPT IP terms.
- **NFR-005 Traceability (Should):** Each reference maps to ≥1 specific claim;
  the citation matrix `Notes` column records which claim/section it supports.
- **NFR-006 Consistency (Should):** Uniform author formatting, title casing,
  venue abbreviations, and arXiv id style across all entries.

---

## 3. System Constraints

- **Technical:** Single-file LaTeX (`proposal/main.tex`), manual `[n]` markers,
  no `.bib` yet. Introducing BibTeX is optional and out of scope unless the list
  grows beyond manageable manual numbering.
- **Source-bound:** Verifiable inputs are limited to `files/` (FOSE preprint,
  doe-genesis.tex, doe-abstract.pdf, amazon.pdf) plus checkable public sources.
- **Business:** Final artifact is the eBay .docx template; deadline
  **2026-09-21**. Compass framing needs Ramesh's confirmation.
- **Regulatory/IP:** eBay royalty-free IP terms; no confidential disclosures.

---

## 4A. Verification Protocol (skill-driven)

Every reference must be cleared by a **verification skill/agent pass** — not by
the author asserting it. The store's `verification` block records the result of
three independent checks per reference:

1. **Exists** — the source resolves: an arXiv id loads, a DOI/URL returns 200, or
   the named file is present in `files/`. (Tooling: WebFetch/WebSearch for public
   sources; filesystem check for local sources.)
2. **No hallucination** — `authors`, `title`, `year`, `venue` in the store match
   the resolved source *exactly*; mismatches fail the check.
3. **Correctly cited** — the proposal claim at each `[n]` is actually supported by
   that source (right paper for the right statement; no misattribution).

Designated verifier: the project's **`review-agent`** (`verify-citations`
command). Its built-in Citation Verification checklist (Exists / Accurate /
Accessible / Cited / Relevant) already implements §4A; it reads `references.json`
as the canonical store and records results back into each `verification` block.
Existence + metadata checks use the literature-review tool (§4B) for public
sources and a filesystem check for local sources. (No constellize skill is used
for this — we own the agents; review-agent is the right home.)

Each `verification` block stores: `{existsCheck, metadataCheck, citationCorrectness,
checkedBy, checkedAt, notes}`. A reference ships only when all three are `pass`.

## 4B. Literature Review Method (Consensus)

When sourcing or validating references (esp. the planned methodology cites
FR-005–FR-009 and confirming FR-002/FR-003 metadata), the literature review
**must use Consensus** — the AI scientific-search engine, via its Claude
integration — as the primary tool to find real papers and ground each claim in
the actual literature. Consensus searches peer-reviewed sources, which directly
supports the no-hallucination requirement (NFR-001).

- **CR-001 (Must):** Each newly added reference is discovered/confirmed through
  Consensus before it enters `references.json` with real metadata.
- **CR-002 (Must):** Consensus output (paper title, authors, year, venue, link)
  is recorded in the entry's `source`/`verification.notes` so the trail is
  auditable.
- **Connectivity:** Consensus is **connected** (`mcp__consensus__search`, user
  scope, OAuth) as of 2026-06-25 — it is the **primary** literature-review tool.
  **Backup only** (if Consensus is unavailable or rate-limited): Hugging Face
  `paper_search` + `WebSearch`/WebFetch against arXiv/DOI, marked as backup in
  `verification.notes` for later Consensus re-confirmation. Note Consensus rate
  limits: batch ≤3 searches at a time; on a rate-limit error, wait ~30s.

## 4C. Prior-Art & Problem Validation (novelty gate)

Before sinking effort into references and the proposal narrative, the literature
review must answer two questions the proposal's credibility depends on — using
Consensus (§4B) as the primary search:

1. **Is this already solved?** Search for existing agentic-KG / code-KG /
   repository-pattern-mining approaches to (deterministic) code generation.
   Identify the **closest competing systems** and exactly what they do.
2. **Are we solving the right problem?** Confirm the framed problem (recurring
   code patterns; weeks→hours; deterministic generation from organizational
   history; PR-validation bottleneck) is **real, valued, and unsolved at the
   scope claimed** — not a strawman or a niche already covered.

**Deliverable:** `llm/construction/requirements/prior-art-analysis.md` containing:
closest related work (with citations), a one-paragraph **gap statement** (what is
genuinely new vs. existing work), and a **verdict**:
- **(a) novel / right problem** → proceed to reference writing;
- **(b) partial overlap** → reposition (state how, and which framing to sharpen);
- **(c) already solved / major overlap** → **STOP and escalate to the user/Ramesh**
  before investing further.

**Requirements:**
- **PA-001 (Must):** Dedicated prior-art search via Consensus on the core claim
  (agentic KG for deterministic code generation) **and** adjacent areas (code
  knowledge graphs, retrieval-augmented code generation, repo-level/issue-driven
  code agents, frequent-pattern mining of code, LLM PR generation & review).
- **PA-002 (Must):** Produce `prior-art-analysis.md` with closest work + gap
  statement + verdict.
- **PA-003 (Must):** If verdict is (c) already-solved / major overlap, **do not
  paper over it** — surface to the user before proceeding.
- **PA-004 (Should):** Feed the closest related work into the reference list
  (these are usually high-impact, Tier-A/B cites) and into the proposal's
  *Previous Work* / *Methodologies* positioning.

This gate runs **first** in execution: novelty is validated before references are
sourced, since a failed verdict changes (or halts) everything downstream.

## 4. Acceptance Criteria

- **AC-001:** All FR-001–FR-004 (Must) satisfied; FOSE and DOE Genesis are
  separate, correctly-targeted entries.
- **AC-002:** Zero orphan entries and zero dangling `[n]` markers (FR-010); list
  renumbered sequentially (FR-011).
- **AC-003:** `citation-matrix.md` updated with every entry; each row has a
  `Verified` status; unverifiable items explicitly flagged (FR-012, NFR-001).
- **AC-004:** Reference count within ~5–8 (NFR-002); each entry traces to a claim
  (NFR-005).
- **AC-005:** `proposal/main.tex` compiles cleanly with the updated references.
- **AC-006:** No eBay-internal detail leaked via any citation (NFR-004).
- **AC-007:** Open items (Compass reference, any unverifiable metadata) collected
  into a single "confirm with Ramesh" checklist for the review pass.
- **AC-008:** Canonical `references.json` exists and is the single source of truth;
  `proposal/main.tex` and `citation-matrix.md` are in sync with it (FR-014).
- **AC-009:** Every shipped reference has all three §4A checks = `pass`; any
  reference not fully passing is `verified: false` and excluded from the final
  draft or explicitly flagged (NFR-001).
- **AC-010:** Each newly sourced reference was found/confirmed via Consensus
  (§4B), with the Consensus trail recorded; backup-only entries are flagged for
  later Consensus re-confirmation (CR-001, CR-002).
- **AC-011:** Impact scores (§1A) recorded for every candidate; Should-tier
  inclusion follows rank within the ~5–8 budget; **excluded candidates logged**
  with score + reason (FR-016).
- **AC-012:** `prior-art-analysis.md` exists with closest related work, a gap
  statement, and a novelty verdict (PA-001, PA-002).
- **AC-013:** If the novelty verdict is "already solved / major overlap," it is
  **surfaced to the user**, not silently absorbed (PA-003).

---

## 5. Priority Summary

| Priority | Requirements |
|----------|--------------|
| **Must** | FR-001, FR-002, FR-003, FR-010, FR-011, FR-012, FR-014, FR-015, FR-016; NFR-001–004; §4A verification; **PA-001, PA-002, PA-003** (novelty gate) |
| **Should** | FR-004, FR-005, FR-006, FR-007, FR-013; NFR-005, NFR-006; PA-004 |
| **Dropped** | ~~FR-008~~, ~~FR-009~~ (2026-06-25) |

## 6. Out of Scope
- Writing the actual reference entries (next step, gated on this spec).
- Migrating to BibTeX.
- Broad literature survey beyond claims already made in the proposal.
