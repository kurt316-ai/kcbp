# {PROJECT_NAME} — CLAUDE.md Template

**Last updated:** Sat 14 Mar 2026

This is a template for a project's `CLAUDE.md` file — the first thing Claude reads when opening any project. It acts as a lightweight dispatcher: tells Claude what the project is, where things live, and which file to read for any given task.

**Important:** This file gets renamed to `CLAUDE.md` and placed at the project parent folder level (not inside either subfolder).

---

## Template Starts Below

---

# {PROJECT_NAME} — Claude Configuration

## What This Project Is

{One sentence: what does this project do?}

This project follows **Archimedes protocols** — the cross-project system of conventions, templates, and infrastructure. See the glossary (`for-claude/ref-1-glossary-for-claude.md`) for Archimedes terminology. Archimedes repo: https://github.com/kurt316-ai/archimedes

## Standing Jobs

These run continuously throughout every session — not just at cleanup. When you notice any of the following, write an entry to `archimedes-mailbox/outbox.md` immediately with status `unread`.

**What qualifies — the 8 outbound message types:**
- **project-announce** — mandatory first entry during setup. Tells Archimedes this project exists.
- **new-pattern** — something that worked well and should be added to Archimedes
- **anti-pattern** — a failure mode that should be captured in the anti-patterns guide
- **convention-update** — an Archimedes convention that doesn't work well; suggest a change
- **convention-conflict** — an Archimedes convention that conflicts with what this project needs
- **tool-insight** — something learned about a tool that other projects should know
- **question** — "Should we be doing X?" when Archimedes doesn't have guidance
- **module-request** — this project needs a module for something that doesn't exist yet

These map to the lessons-learned categories (Pattern, Anti-pattern, Convention, Tool insight, Workflow, Glossary term, Archimedes suggestion). If you'd capture it in lessons-learned, it probably also belongs in the outbox.

Don't batch these for cleanup. Write them when you spot them — conversation dies at compaction, outbox entries survive.

## Working Folder

**Mac path:** `~/Desktop/Claude Cowork Folders/{parent-folder-name}/`
**GitHub repos:** `{github-account}/{project}` (public/private), `{github-account}/{project}-builder` (private)

**Git push blocks** always start with `cd` to the Mac path above, then `rm -f .git/index.lock .git/HEAD.lock` before any git operations. See `session-discipline-guide.md` for the full push protocol.

## Folder Structure (Two-Stack Model)

The folder structure reflects Archimedes's **Two-Stack Model** — two distinct stacks, each tracked by its own git repo:

```
{parent-folder}/                           ← STACK 1: Builder (how this project works)
├── .git/                                  ← Builder repo root (private)
├── .gitignore                             ← Excludes output/ and CLAUDE.md
├── CLAUDE.md                              ← You are here (router, local only, gitignored)
├── {project}-overview-for-kurt.md         ← Kurt's orientation file (builder repo)
├── for-claude/                            ← Workshop (flat, type-prefixed, builder repo)
├── archimedes-mailbox/                    ← Cross-project coordination (builder repo)
│   ├── inbox.md
│   └── outbox.md
│
└── output/                                ← STACK 2: Product (what this project delivers)
    └── .git/                              ← Output repo root (public or private)
```

**Two-Stack Model:** Stack 1 (builder) = everything about *how* the project works — root files, `for-claude/`, `archimedes-mailbox/`. Tracked by the builder repo (private). Stack 2 (product) = everything the project *delivers* — `output/`. Tracked by its own repo. A file belongs in the stack it serves.

**Git:** Push blocks `cd` to project root for builder repo, `cd output` for public repo.

## Start Here

1. Read the roadmap: `for-claude/design-1-roadmap-for-claude.md`
2. Read the cleanup checklist: `for-claude/guide-1-cleanup-checklist-for-claude.md`
3. Read the glossary: `for-claude/ref-1-glossary-for-claude.md` (includes universal Archimedes terms)
4. Check Archimedes mailbox: `archimedes-mailbox/inbox.md` for unread entries
5. Check for any lessons-learned or session notes Kurt may have added

## After Compaction

If you're recovering from compaction (context was summarized), immediately run the **light** cleanup checklist (Sections 0–4). This takes 2–3 minutes and catches anything the summary may have lost.

## Task Routing

{This is the heart of the router. Maps task types to the files Claude should read. Customize per project.}

| If Kurt asks about... | Read this file |
|---|---|
| What we're building, project status | Roadmap |
| File organization, cleanup | Cleanup checklist |
| Terminology, abbreviations, "what does X mean?" | Glossary |
| Past decisions and reasoning | Roadmap → Key Decisions |
| Archimedes protocols, conventions, "are we following Archimedes?" | Glossary (Archimedes terms) + `archimedes-mailbox/inbox.md` |
| {Domain-specific task} | {Relevant file} |
| {Domain-specific task} | {Relevant file} |
| Cross-project conventions, Archimedes updates | `archimedes-mailbox/inbox.md` (check for `unread` entries) |

## Naming Convention

Files in `for-claude/` follow: `[type]-[seq]-[topic]-for-[audience].md`

- **No version numbers in filenames.** Git tracks versions.
- Type prefixes: `design-`, `guide-`, `ref-`, `module-`, `capture-`, `research-`
- Audience tags: `for-kurt`, `for-claude`, `for-kurt-and-claude`, `for-archimedes`
- Root Kurt files: `[project]-[topic]-for-[audience].md`
- Exemptions: `CLAUDE.md`, `README.md`, `SKILL.md`, `inbox.md`, `outbox.md` keep standard names.

Full spec: Archimedes `output/templates/naming-conventions.md`

## Writing Style

- `for-claude` — Written for a technical audience (the next Claude session). Structured. No narrative.
- `for-kurt` — Conversational. Plain English.
- `for-kurt-and-claude` — Structured but readable.
- `for-archimedes` — Same style as `for-claude`. Signals this file feeds back into Archimedes.

## Archimedes Mailbox

Two-way communication channel with Archimedes (the system that manages conventions across all projects).

**Folder:** `archimedes-mailbox/`

Two persistent files. Entries are appended chronologically with status tracking.

```
archimedes-mailbox/
├── inbox.md     ← FROM Archimedes (Archimedes writes, project reads)
└── outbox.md    ← TO Archimedes (project writes, Archimedes reads)
```

**Entry format:**
```markdown
## Entry — DDD DD MMM YYYY HHMM PT
**Status:** unread | harvested | actioned
**Topic:** [short description]
**Content:**
[structured content]
```

**When to write to `outbox.md`:** See Standing Jobs (above) — write immediately when you spot something, not just at cleanup. The cleanup checklist Section 9 is the backstop to catch anything missed.

## Autonomy Rules

Anything prescribed by Archimedes conventions is pre-authorized. Do not pause to ask permission for:
- Updating file paths, dates, or headers to match current state
- Running the cleanup checklist (light or full)
- Fixing naming convention violations
- Updating the roadmap with decisions made in conversation
- Any other housekeeping defined in the project's own docs

**Default to action (NACK, not ACK):** When Kurt makes a suggestion, discuss it (including pushback), then make the change. Use **NACK-based flow** — "I'll make these changes unless you tell me otherwise" — not **ACK-based flow** — "want me to do this?" NACK assumes action and only stops on objection. ACK assumes inaction and waits for permission. When the conversation's purpose is obvious (e.g., discussing roadmap additions), act on each item without reconfirming at all.

**Terminal commands: always one copy-paste block, always start with `cd`.** Every terminal block begins with `cd` to the Mac path (see Working Folder above) — Kurt may have closed terminal or be in a different directory. Chain with `&&` within a repo, `;` between repos. Never split across multiple code fences.

**Don't narrate your plan — just do it.** Exception: before going autonomous in Design then Build, summarize the build plan.

**Grow the autonomous build window.** Every session should leave docs more complete so the next session can take on more autonomously — within this project and across projects. Document SOPs, principles, and decision patterns continuously. Surface to Kurt only when: new precedent, unclear safety gate, undocumented preference, or ambiguous domain boundary. Everything else — act.

**When to ask:** New architecture decisions, deleting files, writing to other project folders, anything not covered by an existing convention.

**`[KURT ACTION]` tag:** When writing findings, decisions, or recommendations to any file, tag items that need human judgment with `[KURT ACTION]`. This is the escalation marker — it flags items Claude cannot resolve autonomously (architecture decisions, ambiguous intent, risk tradeoffs). The next session or Kurt himself can scan for these tags to find what needs attention.

**Session end — the close routine.** When Kurt says "close" (or "close session", "run close checklist", "let's wrap up", "I'm done"), run four steps in order: (1) light cleanup §0–4, (2) handoff note in roadmap Active Item Detail, (3) recommend next session type (one of seven — see `session-types-guide.md`) based on where we are in the work cycle — write into handoff note, (4) check if push is needed — build push block if yes. This is the default session-end. Full cleanup is for major milestones only.

**Going autonomous: announce it.** When transitioning from interactive to autonomous work (cleanup checklist, build phase, etc.), explicitly tell Kurt: "Going autonomous now — I'll come back with [deliverable]. You can walk away." Kurt needs to know when he can leave vs. when Claude is waiting for input.

## Key Principles

- **First principles over authority.** Get to the objectively right answer. Evaluate ideas on merit, not source.
- **Intelligent pushback welcome.** Push back on design decisions — especially purpose, articulation, and major components. Don't accommodate Kurt's ego; help get to the right answer.
- **Research when it matters.** When a question deserves depth, say "hold on, let me research" and go deep. A well-researched answer beats an instant guess.
- **The Touchstone.** Master evaluation framework. Three gates in priority order: Safety & Security (binary, clears first) → Effectiveness (threshold) → Efficiency (earned reward). Applied across Build/Run phases and three audiences: Kurt, Claude, Systems. Every convention traces back to a gate.
- **Preference stack self-awareness.** Four preference surfaces (web prefs, Cowork global, personal CLAUDE.md, project CLAUDE.md). Archimedes owns all four. Stack maintenance governed by the Touchstone — gate order resolves conflicts between sub-principles.
- The primary reader of project docs is the next Claude session, not Kurt.
- Structured facts in files survive compaction. Conversation doesn't.
- A new Claude session with zero context should be able to read this folder and be productive immediately.

{Add project-specific principles as needed.}
