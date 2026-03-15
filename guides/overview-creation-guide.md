# Overview Creation Guide

**Purpose:** Template, quality checklist, and workflow for creating and maintaining overview docs across all Cowork projects.

**When to Load:** Starting a new project, reviewing an overview doc, or updating the roadmap (which keys off the overview's Vision section).

**Audience:** `for-claude` — teaches the next Claude session how to synthesize and maintain overview docs.

**Last updated:** Sat 14 Mar 2026

**Type:** Guide

**Related files:**
- `for-claude/design-1-roadmap-for-claude.md` — overview Vision lifts here; overview Components map to roadmap items.
- `for-claude/ref-5-kurt-design-principles-for-claude.md` — Three Cs apply (Clear → Correct → Coded).
- `naming-conventions.md` — overview docs are root-level Kurt files; naming is `{project}-overview-for-{audience}.md`.

---

## What an Overview Doc Is

An overview doc is Kurt's primary design surface. It captures *what* the project is, *why* it exists, *who benefits*, and *how* the pieces fit together — in language precise enough to guide Claude's work without over-determining implementation. The overview answers the question "if I had 5 minutes and a whiteboard, what would I explain?"

**Touchstone alignment:** Overview docs serve Gate 2 (Effectiveness — clear handoff between Kurt and Claude) and Gate 3 (Efficiency — Kurt explains once, Claude gets it right every time, no clarification loops).

**Gate 1 check:** Overview docs contain no PII, no secrets, no hardcoded credentials. If scope includes integrations (API keys, database URLs), describe them abstractly — specifics live in `.env` and CLAUDE.md, not the overview.

---

## Three Audience Patterns

Choose one pattern for your project. Tradeoff: single doc is simpler; paired/interleaved docs allow audience-specific tuning at a sync cost.

### Option 1: Single Doc, Kurt's Voice (Recommended)

**File:** `{project}-overview-for-kurt.md` at project root.

**Audience:** Primarily Kurt (the human); Claude reads it to understand the project without filters or paraphrase.

**Best for:** Straightforward projects where Kurt's voice and perspective are the clearest way to describe the work.

**Benefit:** One source of truth, no sync tax.

### Option 2: Paired Docs

**Files:**
- `{project}-overview-for-kurt.md` — conversational, Kurt's thinking and rationale.
- `{project}-overview-for-claude.md` — structured, optimized for Claude's understanding.

**Best for:** Highly complex projects where Kurt's rationale needs space and Claude needs a more engineered index.

**Tradeoff:** Both must stay in sync; edit one, verify the other. The Touchstone gates (Clear → Correct → Coded) must apply to both.

### Option 3: Interleaved Sections

**File:** Single doc with audience-labeled sections (e.g., `## Vision (for Kurt and Claude)`, `## Implementation Notes (for Claude only)`).

**Best for:** Close collaboration where Kurt and Claude are co-designing and need to see each other's comments.

**Consideration:** Readable but visually noisier. Scan-ability decreases as section labels accumulate.

---

## Structure Template

This is a floor, not a ceiling. Simple projects stay near the template; complex projects (like Archimedes itself) evolve richer structures. The key: every section below answers a specific, answerable question.

### 1. Title and Metadata

```markdown
# {Project Name}

**Last updated:** {Date in DDD DD MMM YYYY HHMM PT format}
**Word count:** {approx}
**Reading time:** {approx}
```

### 2. What Is {Project Name}?

**One to two sentences.** The elevator pitch. Someone new to the project should read this and know what they're looking at, not *how* it works yet — just what it is.

**Example:** "Archimedes is a living system of templates, conventions, and guides that bootstraps any new Cowork project with Kurt's preferences and maintains a bidirectional connection to every project built with it."

### 3. Touchstone Trace

**Which gates does this project primarily serve?**

Gate 1 is always binary (Safety & Security) and applies everywhere. State the primary gate(s) for this project:

```markdown
**Primary gates:** Gate 2 (Effectiveness — provides the design surface for Kurt-Claude handoff) and Gate 3 (Efficiency — reduces coordination overhead across projects).
```

### 4. Vision

**Three subsections.** Each is 2–3 sentences max. No narrative.

#### What
The concrete outcome. Not aspirational — *deliverable*. "A Python CLI tool" or "a Notion template set" or "a documentation architecture."

#### Why
The problem being solved. Why does this exist? What breaks without it?

#### Who Benefits
End users or stakeholders. Be specific: "Kurt (across all projects)", "Claude (every session)", "leaf projects", "external contractors".

### 5. Scope

#### Definitely In
Things the project owns and will deliver. Bullet points, one-liner each.

#### Definitely Out
Explicit non-goals. As important as what's in — surfaces where responsibility ends. Prevents scope creep.

#### Maybe
Open questions about what belongs to this project. Separate resolved decisions (which go to Open Decisions) from genuine unknowns (which go here).

### 6. How It Works

**2–4 sentences.** System flow at 30,000 feet. Think: "if I sketched this on a whiteboard, what boxes and arrows would I draw?"

**Example:** "Stack 1 (the builder) is where Kurt and Claude work together. Archimedes conventions live here in `for-claude/` working files and root-level design docs. Stack 2 (the product) lives in `output/` and maps to the public repo; it's what new projects download and customize."

### 7. Key Components

**Major pieces of the system.** One-liner per component. Not exhaustive — highlight the ones that matter for understanding how the system holds together.

Example (from Archimedes):
- **Naming conventions** — Metadata-carrying filenames that route Claude to the right file without extra tool calls.
- **Markdown architecture** — Structure-first approach: folder layout and file types tell you what a file is before you read a byte.
- **CLAUDE.md routing** — Local-only configuration that maps questions to files, questions to other projects, and breaks ties between conventions.

### 8. Constraints & Requirements

**Mandatory limitations.** Gotchas that affect design. Budget constraints, tool limitations, non-negotiable architectural decisions.

Examples:
- "Context budget is fixed at 200K tokens per session — overview must fit in 3–5K tokens."
- "All secrets in `.env` — no hardcoded credentials anywhere, including examples."
- "Designed for solo Kurt + async Claude collaboration — not real-time pairing."

### 9. Open Decisions

**Unresolved architectural questions.** Each decision should be answerable — reframe vague questions as concrete scenarios.

**Example of vague:** "How do we handle future integrations?"
**Example of concrete:** "When a new Cowork project needs Notion integration, does Archimedes provide a Notion module template, or does each project build its own integration layer?"

Include:
- **Decision statement** — what's open?
- **Why it matters** — what downstream work depends on this?
- **Candidate answers** — 2–3 options with tradeoffs.

### 10. Kurt's Design Notes

**Verbatim capture.** If Kurt brain-dumped thinking, rationale, or decision history, include it here. Don't paraphrase — quote directly. This is the voice that Claude needs to hear.

Can be structured (numbered points) or raw (conversational prose), depending on what Kurt provided.

---

## Audience Patterns in Action

### For Option 1 (Single Doc, Kurt's Voice)

Structure stays the same. Write in second person where natural ("you'll notice...") but keep the focus on *what the project is* rather than *what you should do*. This is observation, not instruction.

### For Option 2 (Paired Docs)

**Kurt's doc additions:**
- Add a "Rationale" section explaining *why* you made certain scope or design choices.
- Include more context, historical decisions, what was tried and rejected.

**Claude's doc:**
- Leaner. Remove rationale; assume the decision is final.
- More explicit indices and cross-references to other Archimedes docs.
- Structured as a reference Claude might consult multiple times.

### For Option 3 (Interleaved)

Label each section clearly:
- `{Section} (for Kurt and Claude)` — shared understanding.
- `{Section} (for Kurt)` — context, rationale, history.
- `{Section} (for Claude)` — structured index, lookups.

---

## Quality Checklist

Before handing the overview to Kurt, verify:

- [ ] **One clear sentence** answers "what is this project?" Someone unfamiliar could read it and know what they're looking at.
- [ ] **Scope boundaries explicit.** Reviewable in 10 seconds: what's in, what's out, what's unresolved.
- [ ] **Critical constraints captured.** Gotchas, budget limits, architectural non-negotiables are visible, not buried.
- [ ] **Kurt's voice is present.** Paraphrasing away Kurt's thinking leaves you with generic prose. If it sounds like a template, rewrite it.
- [ ] **Touchstone trace is clear.** Which gates does this serve? Anyone reading should know.
- [ ] **No ambiguity on audience.** If Option 2 or 3: audience labels are explicit and consistent.
- [ ] **Token budget respected.** New projects should be 1,500–2,000 words max; mature projects (Archimedes, established systems) may exceed this with review.
- [ ] **Open decisions are answerable.** Not vague philosophy; concrete scenarios with tradeoffs.
- [ ] **No PII, no secrets.** Descriptions only. Specifics live in `.env` and CLAUDE.md.

---

## What to Avoid

**Generic descriptions too vague to guide Claude.** "Build a system for managing things" tells Claude nothing. "Build a Python CLI that reads `.env` credentials and syncs folder structures to Notion, with conflict resolution on name changes" is actionable.

**Missing constraints.**  Hidden gotchas surface during build and derail the plan. Constraint not mentioned = risk unmanaged.

**Over-designed decisions.** Don't lock in implementation when exploration would help. "We'll use PostgreSQL" in the overview might prevent Claude from suggesting SQLite. Say "needs a persistent store" and leave the choice open.

**Buried open questions.** Put them front and center (Section 9). Hidden unknowns look like ignorance.

**Paraphrasing away Kurt's voice.** The overview is a design surface. Kurt's own words and thinking are the content. Rephrasing it "for clarity" often loses the intent.

**Conflating overview with roadmap.** Overview answers *what and why*. Roadmap answers *when, in what order, who does what*. They're separate documents.

---

## Overview as Living Design Surface

The overview is not a static artifact. It's Kurt's working design tool.

- **When Kurt refines language**, treat edits as potential architecture changes, not cosmetic fixes. "Build a Notion template set" vs. "build a Notion template system" — the second implies sustainability and evolution, the first sounds like a one-off. The word choice matters.
- **The Three Cs apply:** Clear → Correct → Coded. The overview is where you verify Clear and Correct before Claude starts Coding.
- **Overview doc = product view; roadmap = build view.** They describe the same thing from different angles. If the overview describes "a CLI tool with config file support," the roadmap might say "Phase 1: basic CLI scaffolding, Phase 2: config file parsing."

---

## Evolution and Maintenance

**New projects:** Use the template as-is. Stick close to the structure.

**Maturing projects:** As projects stabilize, concepts in the overview may grow into dedicated guides or modules. When that happens, extract the concept to a standalone file and leave a cross-reference in the overview. Example:

> Originally the overview had a 300-word section on "Naming Conventions." It became `naming-conventions.md`. The overview now has: "Names follow the conventions in `naming-conventions.md` (system-wide across all surfaces) and `naming-conventions-rationale.md` (why each convention was chosen)."

**Cadence:** Review the overview at major milestones (end of Phase, architectural decision made) or when roadmap decisions contradict the scope. The cleanup checklist includes an overview staleness check.

**Verification:** If Claude is working from the overview and hits ambiguity repeatedly, the overview needs revision. That's feedback on clarity, not on Claude's comprehension.

---

## Relationship to Other Docs

The overview connects to the rest of the Archimedes system:

| Connection | How |
|-----------|-----|
| **Roadmap** | The roadmap's Vision section lifts from the overview's Vision section (What, Why, Who). The roadmap's roadmap items map to overview Components. Open Decisions in the overview become roadmap tasks. |
| **CLAUDE.md routing** | The router file includes: `\| Kurt asks "what is {project}?" \| {project}-overview-for-{audience}.md \|`. This tells the next Claude session where to go. |
| **Architecture decisions** | When an overview Open Decision is resolved, move it to a `design-` file or to CLAUDE.md, depending on scope. Don't leave resolved decisions in the overview. |
| **Markdown architecture** | Overview docs follow the same structural engineering principles as all other Archimedes files (see `markdown-architecture-guide.md`). |

---

## Workflow: Creating an Overview from Scratch

**Input:** Kurt describes the project (brain dump, conversation, existing notes, or all three).

**Process:**

1. **Extract the What, Why, Who.** These three sentences are load-bearing. Get them right before proceeding.
2. **Map major components.** What are the 4–7 core pieces? (More than 7 means you're at the wrong scope level or the overview is trying to do too much.)
3. **Scope boundaries.** Make Kurt's in/out/maybe decisions explicit. Propose scope if unclear; confirm before writing.
4. **Constraints first.** Ask: "What can't change? What would break this?" These are the guardrails.
5. **Write the overview.** Use the template. Stick close to section structure — deviations come later, after the project stabilizes.
6. **Quality checklist.** Run the checklist. Iterate with Kurt on clarity and completeness.
7. **Hand to Kurt.** Overview ready for review and sign-off.

**Estimated time:** 1–2 hours for a straightforward project; complex projects may take longer.

---

## When the Overview Isn't Enough

If the overview reaches 2,500+ words and still feels incomplete, you have two options:

1. **Extract concepts to dedicated guides.** Move "How OAuth integrations work" to a module; leave a one-liner and cross-reference in the overview.
2. **Embrace a richer structure.** Some projects (Archimedes, major platforms, research systems) outgrow the template and develop their own architecture. That's fine — the template is the floor.

In either case, the overview should remain scannable in 5–10 minutes. Complexity belongs in supporting docs, not in the overview itself.
