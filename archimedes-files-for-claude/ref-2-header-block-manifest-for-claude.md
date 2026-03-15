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

## guide-*-cleanup-checklist-for-claude.md

```markdown
# {PROJECT_NAME} — Cleanup Checklist

**Last updated:** {DDD DD MMM YYYY HHMM PT}

**Two modes:** Light (after compaction, 2–3 min), Close (end of session, 3–5 min), Full (before major push, 10–15 min). Every section tagged [Light], [Full], or both.

**Natural triggers:** compaction recovery → Light. Kurt says "close"/"wrap up" → Close. Kurt says "let's push"/"run the cleanup checklist" → Full.

**Design principle:** Human input first (Sections 0–1 require Kurt), then Claude runs autonomously. Kurt can walk away after Section 1.

**Section order:** §0 Self-Check → §1 Kurt Input → §2 Roadmap Sync → §3 Context Preservation → §4 Mailbox Check → §4.5 Audit Feedback → [Light stops] → §5+ Full mode sections.
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
