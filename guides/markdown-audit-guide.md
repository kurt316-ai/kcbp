# Markdown Audit Guide

**Purpose:** Operational checklist for auditing markdown files against architecture principles and file-type optimization rules. Use this to grade every file in a project, identify violations, and produce a migration plan.
**Audience:** `for-claude`
**Prerequisites:** Read `markdown-architecture-guide.md` (13 principles) and `file-type-optimization-guide.md` (10 types + 5 cross-cutting principles) first. This guide operationalizes those principles into a repeatable audit protocol.
**Last updated:** Fri 14 Mar 2026

**Touchstone trace:** Gate 2 (files correctly encode human intent → Claude behaves correctly) + Gate 3 (minimal tokens, right types, no bloat). Gate 1 check: audit must flag any PII or secrets found during file reads.

---

## When to Run

- **Scheduled:** As part of the full cleanup checklist (Section 5 expanded). Quarterly deep audit recommended.
- **Triggered:** When context feels bloated, when Claude repeatedly loads files it doesn't need, or when a design session identifies structural drift (as in the current session).
- **Post-migration:** After any bulk file restructuring, run the audit to verify the migration achieved its goals.

---

## The Audit Protocol

### Phase 1: Inventory and Measure

**Goal:** Produce a complete file inventory with type classification, token counts, and budget compliance.

**Steps:**

1. **List all markdown files** with word counts. Estimate tokens at ~1.33× word count.
2. **Classify each file** by type using the Type Identification Flowchart (file-type-optimization-guide).
3. **Record budget compliance** for each file:

| Classification | Budget | Review zone | Mandatory action zone |
|----------------|--------|-------------|----------------------|
| Router (project) | <500 ideal | 500–1,000 | >1,000 |
| Router (personal) | <1,500 | — | >1,500 |
| Design surface | 3,000–5,000 | 5,000–6,000 | >6,000 |
| Guide | 1,000–3,000 | 3,000–4,000 | >4,000 |
| Principles document | 3,000–6,000 | 6,000–8,000 | >8,000 |
| Reference | <5,000 | 5,000–6,000 | >6,000 |
| Module | 1,000–3,000 | 3,000–4,000 | >4,000 |
| Capture file | <5,000 total | 5,000–6,000 | >6,000 or >10 unharvested entries |
| Template | Matches target type | — | Exceeds target type |
| Research | 2,000–4,000 | 4,000–5,000 | >5,000 |
| Mailbox entry | <3,000 | 3,000–4,000 | >4,000 |
| Root Kurt file (overview) | 2,000–4,000 | 4,000–6,000 | >6,000 |
| Root Kurt file (system guide) | 2,000–4,000 | 4,000–6,000 | >6,000 |
| Root Kurt file (roadmap active) | 3,000–6,000 | 6,000–8,000 | >8,000 |

4. **Flag files in review or mandatory action zones** — these are the migration candidates.

### Phase 2: Per-File Grading

For each file (or at minimum, each file flagged in Phase 1), grade against these criteria. Score: **Pass**, **Review** (not wrong but could improve), **Fail** (violates a principle).

#### A. Type Correctness

| Check | Principle | Score |
|-------|-----------|-------|
| Is the file classified as the right type? (Use the flowchart) | Type Identification | |
| Does the filename prefix match its actual type? | Type Prefix = Optimization Contract | |
| If `ref-` prefix: is it actually a reference (lookup table) or a principles document (read end-to-end)? | Principles vs. Reference disambiguation | |
| If the file spans two types, should it be split? | "If a file spans two types, it's usually a sign it should be split" | |

#### B. Token Budget

| Check | Principle | Score |
|-------|-----------|-------|
| Is the file within its type's budget? | Architecture Principle #3 (Token Budget) | |
| If over budget: are there extractable sections? Apply the four extraction triggers. | Extraction Triggers (cross-cutting) | |
| For growing files: is active content >30% of total? | Active vs. Archive Separation | |
| For growing files: have harvest triggers been met? | Harvest Cadence | |

#### C. Structure

| Check | Principle | Score |
|-------|-----------|-------|
| Does the file start with Purpose + When to Load + Core instructions? | Architecture Principle #8 (Standard Internal Structure) | |
| Are the first 3–5 lines the highest-value content? | Architecture Principle #4 (Front-Load) | |
| If over 3,000 tokens: does it have internal navigation (mini-TOC, section separators)? | Architecture Principle #10 (Internal Navigation) | |
| If it has archive content: is there a skip marker? | Architecture Principle #10 + #11 | |
| Is the writing style correct for its audience tag? | Architecture Principle #5 (Declarative Over Narrative) | |

#### D. Dependencies and Cross-References

| Check | Principle | Score |
|-------|-----------|-------|
| Can Claude follow this file without loading others? (Or are prerequisites stated?) | Self-containment test (Guide, Module types) | |
| Are cross-references pointing to files that actually exist? | Stale route check | |
| Is this file routed from CLAUDE.md or the cleanup checklist? | Architecture Principle #6 (Conditional Loading) | |
| If this is a principles document: does it have a Propagation Targets table? | Principles Document type rules | |

#### E. Content Quality

| Check | Principle | Score |
|-------|-----------|-------|
| Does every section earn its tokens? (Would removing it cause wrong behavior?) | Dual Optimization | |
| Are critical facts in tables/key-value pairs, not buried in prose? | Anti-pattern #3 (Long unstructured prose) | |
| Is the `Last updated` date current? | Stale Content | |
| For `for-claude` files: is the writing declarative, not narrative? | Architecture Principle #5 | |
| For `for-kurt` files: is the writing conversational and readable? | Audience optimization | |

### Phase 3: Produce Migration Plan

After grading, produce a migration plan organized by priority:

**Priority 1 — Mandatory action (Fail scores):**
- Files over mandatory action threshold
- Wrong type classification
- Missing from router
- PII/security findings

**Priority 2 — Review items (Review scores):**
- Files in review zone (approaching budget)
- Missing internal navigation on large files
- Missing extraction candidates
- Unharvested capture files

**Priority 3 — Optimization (all Pass, but improvements possible):**
- Files that could benefit from archive separation
- Cross-reference improvements
- Style consistency fixes

**Migration plan format:**

```
## Migration Item [seq]

**File:** {path}
**Current state:** {type, token count, key finding}
**Action:** {specific action — split, extract, archive, retype, restructure}
**Depends on:** {other migration items that must complete first}
**Estimated effort:** {small/medium/large}
```

### Phase 4: Verify Migration

After the Build session executes the migration:

1. Re-run Phase 1 (inventory and measure). Verify all files are within budget.
2. Spot-check 5 migrated files against Phase 2 grading criteria.
3. Verify all cross-references still resolve (no broken links from moves/renames).
4. Verify router (CLAUDE.md) routes to all new/renamed files.
5. Run one cold-start test: could a new Claude session navigate from CLAUDE.md to the right file for a typical task?

---

## Quick Audit (Lightweight Alternative)

For routine checks (not a full migration audit), run this abbreviated version:

1. `wc -w` all markdown files. Estimate tokens. Flag anything over its type ceiling.
2. Check the 3 largest files: right type? extraction candidates?
3. Check capture files: harvest needed?
4. Check router: any missing routes for new files?

Time: 5–10 minutes. Catches the highest-impact issues.

---

## Cross-References

**Part of the three-doc architecture package + audit companion:**
- `markdown-architecture-guide.md` → 13 structural principles graded against
- `file-type-optimization-guide.md` → 10 types + 5 cross-cutting principles graded against
- `naming-conventions.md` → filename compliance (checked separately in cleanup checklist Section 6)
- **This doc** → operational protocol for running the audit

**Related:**
- Cleanup checklist → Full mode Section 5 references this guide for expanded file inventory
- `anti-patterns-guide.md` → failure examples that inform grading criteria
- `ref-8-audit-framework-for-kurt-and-claude.md` → Archimedes-specific audit framework (broader scope than markdown-only)
