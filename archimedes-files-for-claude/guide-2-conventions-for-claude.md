# Naming & Writing Conventions

**Source:** Archimedes canonical push. Do not edit — updates come from Archimedes.
**Audience:** `for-claude` — file naming, writing style, folder structure rules.

---

## File Naming

Files in `{project}-files-for-claude/` follow: `[type]-[seq]-[topic]-for-[audience].md`

- **No version numbers in filenames.** Git tracks versions.
- **Type prefixes:** `design-`, `guide-`, `ref-`, `module-`, `capture-`, `research-`
- **Audience tags:** `for-kurt`, `for-claude`, `for-kurt-and-claude`, `for-archimedes`
- **Root Kurt files:** `[project]-[topic]-for-[audience].md`
- **Exemptions:** `CLAUDE.md`, `README.md`, `SKILL.md`, `inbox.md`, `outbox.md` keep standard names.

Full spec: Archimedes `output/templates/naming-conventions.md`

## Folder Structure

Every Archimedes project has two instruction subfolders split by ownership:

```
{Project}/
├── CLAUDE.md                          ← thin router (project identity + routing)
├── archimedes-files-for-claude/       ← owned by Archimedes, one-way push
├── archimedes-mailbox/                ← bidirectional feedback channel
├── {project}-files-for-claude/        ← project-specific files
├── {project}-overview-for-kurt.md     ← Kurt's orientation
└── output/                            ← product deliverables (when applicable)
```

**`archimedes-files-for-claude/`** — Owned entirely by Archimedes. One-way push. Contains behavioral instructions (how to work). When Archimedes evolves, this folder gets overwritten wholesale. The project never touches it.

**`{project}-files-for-claude/`** — Owned entirely by the project. Contains project-specific context (what to work on): roadmap, glossary, cleanup checklist, domain guides, capture bin. Normal project workflow.

**`archimedes-mailbox/`** — Bidirectional feedback channel. Different purpose from instruction push.

## Two-Stack Model

Stack 1 (builder) = everything about *how* the project works — root files, `{project}-files-for-claude/`, `archimedes-files-for-claude/`, `archimedes-mailbox/`. Tracked by the builder repo (private).

Stack 2 (product) = everything the project *delivers* — `output/`. Tracked by its own repo (when applicable).

## Writing Style

- `for-claude` — Written for a technical audience (the next Claude session). Structured. No narrative.
- `for-kurt` — Conversational. Plain English.
- `for-kurt-and-claude` — Structured but readable.
- `for-archimedes` — Same style as `for-claude`. Signals this file feeds back into Archimedes.

## Kurt's Prose Style (for human-facing text)

- **Numbered outline form** where relevant.
- **Lists follow a logical order.** Defaults: priority order (thinking), sequential order (doing). Any intentional logic works.
- **Max 3 wrapped lines per paragraph.** Split if longer.
- **Enumerate, don't embed.** Break paragraph lists into numbered outline form.
- **Bold key words** to make them pop.
- **Key points format:** **1–5 word bold prefix**, colon, description.
- **Why subbullets.** When stating we're doing something, add a *Why* subbullet with the reason.
