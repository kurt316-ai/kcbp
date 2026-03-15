# Header Block Manifest

**Source:** Archimedes canonical push. Do not edit — updates come from Archimedes.
**Audience:** `for-claude` — used during install, push, and self-audit to verify project file headers.

Each section below contains the canonical header block for one project file type. During a push or audit, compare the project file's header (everything above the separator) against the block here. If they differ, replace the project's header with the canonical version. Never touch content below the separator.

**Separator:** `<!-- ARCHIMEDES HEADER END — do not edit above this line -->`

**Keying:** Headers are matched by filename pattern (file type + topic), not by sequence number. A project may have `capture-1-idea-bin` or `capture-3-idea-bin` — the header is the same.

---

## design-*-roadmap-for-claude.md

```markdown
# {PROJECT_NAME} — Project Roadmap

**Last updated:** {DDD DD MMM YYYY HHMM PT}
**Audience:** `for-claude` — Kurt engages with this doc through conversation, not by reading it directly. Optimize for Claude answering "what's next?" and "what was decided about X?"

**Structure:** What's Next (priority queue) → Active Item Detail → Vision → Components → Phases → Open Questions → Decision Log → Kurt's Notes Capture → How Claude Uses This Doc.

**Rules:**
- What's Next: max 7 active items. Two numbering systems: Seq (execution order, mutable) and ID (permanent, for cross-refs).
- Status values: `not-started` · `in-progress` · `blocked` · `done`. Done items: Seq = `—`. Parked: Seq = `P`.
- Decision Log: append-only, sequential. Never reorder. Later decisions reference earlier ones with "Updates #X".
- Active Item Detail: pruning rule — when an item reaches `done`, collapse to a one-liner pointing at the deliverable.
- Every session: check priorities, move done items, add decisions, capture Kurt's thinking, update timestamp.
- Relationship to overview doc: roadmap = top-down view of the build (process). Overview = top-down view of the product.
```

<!-- ARCHIMEDES HEADER END — do not edit above this line -->

---

## guide-*-project-health-checklist-for-claude.md (filename: guide-1-cleanup-checklist-for-claude.md)

```markdown
# {PROJECT_NAME} — Project Health Checklist

**Last updated:** {DDD DD MMM YYYY HHMM PT}

**Purpose:** Comprehensive audit for keeping project files, conventions, and documentation in sync. The full project health check — "is the project clean?"

**When to run:** Before major push with many changes. When Kurt asks for it. Not for routine session close or compaction recovery — those have their own checklists in guide-1.

Three checklists exist, each serving a different purpose:

| Checklist | Where it lives | When to run | Purpose |
|---|---|---|---|
| **Session Close** | `archimedes-files-for-claude/guide-1` § "Session Close Checklist" | Kurt says "close" | Wrap up session. Self-contained. Autonomous. |
| **Recovery** | `archimedes-files-for-claude/guide-1` § "Recovery Checklist" | After compaction | Verify critical state survived context loss. |
| **Project Health** | This file | Before major push, on request | Full audit: files, naming, style, stale content, repos. |

**Natural triggers:**
- Kurt says "let's push" / "run the health check" / "run the full checklist" → **This file.**
- Kurt says "close" / "wrap up" → **Not this file.** Go to guide-1 Session Close.
- Compaction recovery → **Not this file.** Go to guide-1 Recovery Checklist.
```

<!-- ARCHIMEDES HEADER END — do not edit above this line -->

---

## ref-*-glossary-for-claude.md

```markdown
# {PROJECT_NAME} — Glossary

**Last updated:** {DDD DD MMM YYYY HHMM PT}

Use these terms consistently across all project files. When in doubt, check here first. Prevents Claude from hallucinating meanings or using inconsistent terminology across sessions.

**Structure:** Archimedes Terms (universal, keep as-is) → Domain Terms → Project-Specific Terms → People & Accounts → Technical Terms.

**Rules:**
- Retired terms stay with a note: `Retired. Use {new term} instead.` Don't delete — future sessions might encounter the old term.
- Cross-project terms: add to lessons-learned under **Glossary term** category for Archimedes harvest.
- Update when: new term comes up that Claude might misinterpret, Kurt corrects a term, a term is retired or renamed.
```

<!-- ARCHIMEDES HEADER END — do not edit above this line -->

---

## capture-*-idea-bin-for-kurt-and-claude.md

```markdown
# {PROJECT_NAME} — Idea Bin

**Last updated:** {DDD DD MMM YYYY HHMM PT}
**Type:** Capture file
**Purpose:** Raw thoughts, ideas, components, and design decisions in progress. Append-only. Persistent throughout the project.

**How to use:** Append entries at the bottom. Date them. No structure required — thoughts can be rough, incomplete, or half-baked. Typical entries: vision, use cases, features, constraints, open questions, design decisions, worries.

**Synthesis:** When ready to turn ideas into an overview doc + roadmap, tell Claude "ready to synthesize the idea bin." See `idea-bin-synthesis-guide.md` for the full process.
```

<!-- ARCHIMEDES HEADER END — do not edit above this line -->

---

## ref-*-constraints-for-claude.md

```markdown
# {PROJECT_NAME} — Constraints & Rules

**Last updated:** {DDD DD MMM YYYY HHMM PT}

Hard rules Claude must follow in this project. Non-negotiable — not suggestions, not best practices. If something here conflicts with Claude's default behavior, this file wins.

**Structure:** Formatting Rules → Technical Constraints → Content Rules → Security Rules → Process Rules.

**Rules:**
- Each constraint must be specific enough to act on. "Write good code" is not a constraint. "All Python functions must have docstrings" is.
- Read at the start of every session. These override defaults.
- If a constraint seems wrong or outdated, flag it to Kurt — don't silently ignore it.
```

<!-- ARCHIMEDES HEADER END — do not edit above this line -->
