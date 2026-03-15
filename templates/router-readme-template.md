# {PROJECT_NAME} — CLAUDE.md Template

**Last updated:** Sat 14 Mar 2026

This is a template for a project's `CLAUDE.md` file — the first thing Claude reads when opening any project. It acts as a lightweight router: tells Claude what the project is, where things live, and which file to read for any given task.

**Important:** This file gets renamed to `CLAUDE.md` and placed at the project root (not inside either subfolder).

## What Makes an Archimedes Project

Three things turn a folder into an Archimedes-compliant project:

1. **Archimedes files pushed.** The `archimedes-files-for-claude/` folder contains canonical behavioral instructions — session protocols, autonomy rules, conventions, mailbox protocol, key principles. These files are owned by Archimedes and overwritten wholesale on each push. The project never edits them.

2. **Standard folder structure.** Every project has the same top-level layout:
   - `archimedes-files-for-claude/` — Archimedes-owned, read-only for the project
   - `{project}-files-for-claude/` — project-owned (roadmap, glossary, cleanup checklist, domain files)
   - `archimedes-mailbox/` — bidirectional communication with Archimedes (inbox + outbox)
   - `CLAUDE.md` — thin router at root

3. **Thin CLAUDE.md with Archimedes routing.** Project identity up top, then routing pointers to both folders (with the read-only rule on the Archimedes folder), then project-specific additions below. All behavioral instructions live in the pushed files — CLAUDE.md just points to them.

---

## Template Starts Below

---

# {PROJECT_NAME} — Claude Configuration

{One sentence: what does this project do?}

This project follows **Archimedes protocols**. Archimedes repo: https://github.com/kurt316-ai/archimedes

## How to Work — `archimedes-files-for-claude/`

Read these files for behavioral instructions (session protocols, autonomy, conventions, mailbox, principles). Owned by Archimedes — **never edit these files.** If you find errors, conflicts, or improvements, write to `archimedes-mailbox/outbox.md` instead.

## What to Work On — `{project}-files-for-claude/`

Read these files for project-specific context (roadmap, glossary, cleanup checklist, domain guides).

## Working Folder

**Mac path:** `~/Desktop/Claude Cowork Folders/{parent-folder-name}/`
**GitHub repos:** `{github-account}/{project}` (public/private), `{github-account}/{project}-builder` (private)

## Folder Structure

```
{parent-folder}/
├── CLAUDE.md                          ← You are here (thin router)
├── archimedes-files-for-claude/       ← Owned by Archimedes, one-way push (read-only)
├── archimedes-mailbox/                ← Cross-project coordination
│   ├── inbox.md
│   └── outbox.md
├── {project}-files-for-claude/        ← Project-specific files
├── {project}-overview-for-kurt.md     ← Kurt's orientation file
└── output/                            ← Product stack (when project delivers)
```

{If the project only has a builder stack, note that here. Example: "Single-Stack (Builder only): {project} currently has only Stack 1."}

## Start Here

1. Read behavioral instructions: `archimedes-files-for-claude/` (all files, **read-only**)
2. Read project context: `{project}-files-for-claude/` (roadmap, glossary, cleanup checklist)
3. Check Archimedes mailbox: `archimedes-mailbox/inbox.md` for unread entries
4. Check for any lessons-learned or session notes Kurt may have added

## Task Routing

{The heart of the router. Maps task types to files. Customize per project.}

| If Kurt asks about... | Read this file |
|---|---|
| What we're building, project status | Roadmap |
| File organization, cleanup | Cleanup checklist |
| Terminology, abbreviations, "what does X mean?" | Glossary |
| Past decisions and reasoning | Roadmap → Key Decisions |
| Archimedes protocols, conventions | `archimedes-files-for-claude/` |
| Cross-project conventions, Archimedes updates | `archimedes-mailbox/inbox.md` (check for `unread` entries) |
| {Domain-specific task} | {Relevant file} |
| {Domain-specific task} | {Relevant file} |

## Project-Specific Principles

{Add domain boundaries, interface notes, and any principles unique to this project. Examples:}

{- **Domain boundary:** {project} owns X. {other project} owns Y. Don't let {project} creep into Y.}
{- **Claude interface:** Cowork is the default. For deep codebase work, route to Claude Code.}
