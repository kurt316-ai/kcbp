# Markdown Architecture Guide

**Purpose:** Translation rules that govern how human-facing principles and SOPs become Claude-optimized markdown files. Every file costs context budget — these rules ensure the translation is both effective (right behavior) and efficient (minimal tokens).
**Audience:** `for-claude`
**Companion doc:** `archimedes-system-guide-for-kurt.md` (project root) Part 1 has human-readable explanations of these same principles.
**Last updated:** Fri 14 Mar 2026

**Touchstone trace:** Gate 2 (effective handoff — Claude reads correctly, Kurt scans quickly, Systems parse reliably) + Gate 3 (minimal tokens, right file type, front-loaded for compaction resilience). Gate 1 check: no secrets in file names or paths, no PII in public-facing file structures.

## When to Load

- Creating or restructuring a markdown file
- Running a reconciliation cycle
- Setting up a new project's file architecture
- Auditing file structure
- Translating a new principle or SOP into Claude-facing files

---

## The Three-Layer Model

Archimedes operates across two layers with a translation mechanism between them:

**Human layer** — optimized for human expression and comprehension. Contains 4 Design Principles (`ref-5`) and 23 SOPs (`ref-6`). This is WHAT Kurt wants — stated in his language, organized by his mental model.

**Claude layer** — optimized for token efficiency and Claude consumption. Contains ~57 markdown files, each following its type's optimization contract (`file-type-optimization-guide.md`). This is THE OPERATIONAL REALITY — what Claude actually reads and acts on.

**Translation** — the one-to-many mapping from human intent to Claude files. One human SOP may need to live in 8 different files, each encoded in the form appropriate to that file's type (one-liner in a router, full paragraph in a guide, failure mode in the anti-patterns guide, definition in the glossary). The translation is governed by:

- **This guide** — the 13 structural principles below. HOW content is encoded in any file.
- **File type optimization guide** — the 10 type-specific contracts + 5 cross-cutting principles. WHAT form content takes per file type.
- **SOP registry** (`ref-6`) — the mapping table. WHERE each SOP lives and at what tier.

**The translation pipeline:**

1. Kurt states a principle or SOP (human layer)
2. Classify: which tier? which files? (SOP registry)
3. Encode: write to each file in the form its type requires (this guide + file type guide)
4. Verify: cleanup checklist confirms translation is correct and current

**Why this matters:** a principle that lives only in the human layer (conversation, overview doc) is aspirational. A principle that has been translated into the right Claude-facing files is operational. The gap between the two is where conventions die.

---

## Principles

### 1. Root Files Route, Don't Store

Root file = always-on budget. Contains: identity (2–3 sentences), routing logic, autonomy rules. Does NOT contain: preferences, conventions, technical knowledge, or anything that could live in a conditional file.

**Test:** Could any task skip this info? → Doesn't belong in root.

### 2. Proximity — Info Lives Where It's Consumed

>80% of tasks need it? → Always-on. Specific task type? → That task's file. Specific project? → That project's file.

**Corollary — output-shaping conventions:** Any convention that governs how Claude formats output for Kurt (push blocks, response style, naming) must live on a path Claude walks after every compaction (CLAUDE.md or cleanup checklist). If it only lives in an on-demand guide, post-compaction Claude won't know it exists until someone loads that guide.

### 3. Token Budget

| Range | Action |
|-------|--------|
| Under 1,000 | Inline into parent file |
| 1,000–3,000 | Ideal. Target this range. |
| 3,000–5,000 | Review for split opportunity |
| Over 5,000 | Mandatory split |

Cohesion overrides budget — a natural 4,000-token file beats two awkward 2,000-token splits.

### 4. Front-Load

First 3–5 lines = highest-value instructions. Two reasons:

1. **Attention gradient:** Early content has marginally stronger influence when context is heavy.
2. **Compaction resilience:** Summaries of file reads preserve openings better than middles.

**Order:** Purpose → "Never do X" rules → Core instructions → Context/rationale → Cross-references.

### 5. Declarative Over Narrative

`for-claude` files: short, direct, no filler. Every extra word burns tokens.

`for-kurt` files: natural prose, explanatory. Different rule.

### 6. Conditional Loading

Root file = decision tree. Match current task → load relevant files only.

Cascading subrouters for complex domains: top-level router → domain router → specific files.

### 7. File Names = Free Metadata

`[what-it-is]` in the naming convention lets Claude route from a directory listing without opening files. Make it specific.

### 8. Standard Internal Structure

1. Purpose line
2. When to load (trigger condition)
3. Core instructions (front-loaded)
4. Cross-references
5. Last reconciled (date)

### 9. One SOP, Many Implementation Points (Rosetta Stone)

A single Kurt-facing SOP (e.g., "always use NACK") maps to multiple Claude-facing implementation points — definition in glossary, prescription in router template, behavior in session discipline guide, failure mode in anti-patterns guide, always-on in personal CLAUDE.md, etc.

**Tiered encoding (see Design Principle #4 — Dual Optimization):** Not every implementation point carries full text. SOPs are tiered:

- **Tier 1 (always-on):** Universal SOPs that apply to every interaction. These live inline in routers as brief one-liners because they must survive every compaction on every surface.
- **Tier 2 (domain-loaded):** Domain-specific SOPs that live in their domain files (guides, modules). Loaded by the cleanup checklist or on-demand when the task context requires them.

The SOP registry (in the private builder repo) tracks each SOP's tier and full propagation list.

**Implication for file changes:** When a convention changes, check the SOP registry for the full propagation list. A single-file update is almost always incomplete.

**Implication for new conventions:** When Kurt states a new SOP, two questions: (1) which tier? (2) which files does this need to live in?

### 10. Internal Navigation

Files over 3,000 tokens need navigable structure beyond front-loading. Front-loading (#4) ensures the opening is high-value; internal navigation ensures Claude can efficiently access the middle.

**Mini-TOC:** After the purpose/metadata block, add a `## Contents` section with numbered section names. Not every sub-section — just the major structural divisions.

**Section separators:** Use `---` horizontal rules between major sections. These give Claude visual landmarks for partial reads and enable "read until the next `---`" patterns.

**Skip markers:** For files with archive/historical sections, add `<!-- ACTIVE CONTENT ENDS HERE -->` so Claude knows when to stop for routine tasks. This is especially important for roadmaps and capture files.

**When NOT to add navigation:** Files under 3,000 tokens. Adding a TOC to a 1,500-token guide wastes tokens and adds maintenance burden. The front-loading principle is sufficient for smaller files.

### 11. Active vs. Archive Separation

Files that grow by accumulation (roadmaps, captures, registries, decision logs) develop a mix of current and historical content. Without separation, Claude loads history it doesn't need, wasting context budget.

**The 30% rule:** When the active portion of a growing file drops below 30% of total tokens, the file needs separation.

**Two patterns:**
1. **Companion archive file:** Move historical content to `{filename}-archive.md`. The active file stays lean. The archive loads only when provenance matters.
2. **Internal archive section:** Add `## Archive` at the bottom with a skip marker above it. Simpler for smaller files, but doesn't save tokens when the full file is loaded.

**Applies to:** Roadmap decision logs, capture files past harvest, references with deprecated entries, design surfaces with historical context.

### 12. Extraction Triggers

Design surfaces and other source-of-truth files shed content as concepts mature. This is how the file system stays lean: the design surface holds raw thinking → concepts stabilize → they get extracted to their target file type → the design surface keeps a cross-reference.

**Four concrete triggers** (see file-type-optimization-guide § Extraction Triggers for the full protocol):
1. **Token budget trigger** — file exceeds type ceiling
2. **Stability trigger** — section unchanged for 3+ sessions
3. **Frequency trigger** — Claude loads the file primarily for one section
4. **Dependency trigger** — other files reference a specific section

**The extraction pipeline is a checkpoint, not a suggestion.** The cleanup checklist (Full mode, Section 5) must include a token budget check for all files against their type ceilings.

### 13. Root File Budgets

Human-layer files (overview docs, system guides, roadmaps) compete for the same context budget as Claude-layer files. The file-type guide covers `for-claude/` types; this principle extends budget discipline to root files.

**Budgets:** Overview doc: 2,000–4,000 tokens. System guide: 2,000–4,000 tokens. Roadmap active portion: 3,000–6,000 tokens. See file-type-optimization-guide § Root Kurt File Budgets for the full table.

**The pattern:** Root files are optimized for Kurt's editing experience. When they grow past budget, the fix is extraction to focused `for-claude` guides — not restructuring the root file for Claude's consumption. The root file stays in Kurt's voice; the extracted guide is optimized for Claude.

---

## When to Use Paired Documents

Paired documents (decision #86) work when the two audiences have **separate interaction patterns** with the content. Decision criteria:

| Condition | Result |
|-----------|--------|
| Kurt never reads the file directly (engages via conversation) | Split. Claude-optimized version only; Kurt version optional. Example: roadmap. |
| Kurt actively writes/edits the file AND Claude reads it | Don't split. One source of truth (for-kurt). Extract focused for-claude guides as concepts mature. Example: overview doc. |
| Both audiences read but neither actively edits | Split. Each version optimized for its reader. Example: markdown architecture guide. |

**Key risk of splitting an actively-edited file:** sync tax. Every Kurt edit must flow to the Claude version. If sync slips, two versions of the truth diverge — worse than one slightly verbose file.

**Better pattern for design surfaces:** overview doc stays for-kurt (the source of truth). When a principle matures into an operational rule, extract it into a focused for-claude guide. The overview spawns guides; it doesn't get a shadow copy.

---

## Reconciliation Cycle

**Cadence:** Weekly or when context feels bloated. For a full operational protocol, see `markdown-audit-guide.md`.

1. **Audit always-on files** — apply 80% test, demote to conditional
2. **Check `<!-- TEMP -->` tags** — move content to proper home if it now exists
3. **Token budget check** — flag files over their type-specific ceiling (not just a flat 5,000). Check both `for-claude/` files AND root Kurt files against the budgets in the file-type-optimization-guide.
4. **Extraction check** — for any file in the review-for-extraction zone, apply the four extraction triggers (token budget, stability, frequency, dependency). Execute extraction or document why it's deferred.
5. **Archive check** — for growing files (roadmaps, captures, registries), check the 30% active content rule. Separate active from archive where needed.
6. **Harvest check** — capture files and mailbox entries past their harvest triggers. Process and update statuses.
7. **Pull learnings** — new patterns or anti-patterns to capture
8. **Prune stale** — past-phase content, superseded decisions

**`<!-- TEMP -->` convention:** Mark misplaced content with `<!-- TEMP: belongs in [file] -->`. Reconciliation cycle processes the queue.

---

## Cross-References

**Part of the four-doc architecture package:**
- `naming-conventions.md` → how files are named and organized (system-wide, all surfaces)
- `file-type-optimization-guide.md` → type-specific constraints layered on top of these general principles
- **This doc** → structural engineering principles for all markdown files
- `markdown-audit-guide.md` → operational checklist for auditing files against these principles

Other references:
- `markdown-audit-guide.md` → operational checklist for auditing files against these principles
- Overview doc Design Principle #5 → references this guide
- Router README template → implements #1 and #6
- Cleanup checklist → reconciliation cycle maps to full-mode pass
- Session discipline guide → runtime complement (when to checkpoint/unload)

## New Project Application

1. Build decision tree → what files exist on disk
2. This guide → how files are structured internally
3. Task router in CLAUDE.md → implements conditional loading (#6)
4. Reconciliation cycle → ongoing architecture hygiene
