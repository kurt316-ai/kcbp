# Archimedes — Best Practices for Kurt & Claude

Conventions and infrastructure for all of Kurt's Cowork projects. Archimedes evolves best practices, pushes them to every project, and absorbs lessons learned back — so problems get solved once.

---

## START HERE

**New project:**
1. Create a project folder on your desktop
2. Copy the **entire contents** of `START HERE - new project/` into it (CLAUDE.md, project-files-for-claude/, archimedes-mailbox/, .gitignore)
3. Open Cowork, point it at the folder — Claude takes it from there

**Existing project:**
1. Copy `CLAUDE-update.md` from `START HERE - existing project/` into your project folder
2. Open Cowork and tell Claude: "Read CLAUDE-update.md and follow the instructions"

---

## What's in this repo

```
archimedes/
├── archimedes-files-for-claude/          ← Distribution folder — what projects pull
├── START HERE - new project/              ← Greenfield install seed
│   ├── CLAUDE.md                         ← Seed router (Claude replaces during setup)
│   ├── .gitignore                        ← Standard exclusions
│   ├── project-files-for-claude/         ← Seed project files (Claude renames to {project}-files-for-claude/)
│   │   ├── capture-1-idea-bin-for-kurt-and-claude.md
│   │   ├── guide-1-cleanup-checklist-for-claude.md
│   │   └── ref-1-glossary-for-claude.md
│   └── archimedes-mailbox/               ← Seed mailbox
│       ├── inbox.md
│       └── outbox.md
├── START HERE - existing project/         ← Brownfield retrofit instructions
│   └── CLAUDE-update.md
└── README.md                             ← You are here
```

**`archimedes-files-for-claude/`** is the canonical distribution folder. Every Archimedes project copies this folder locally and reads it at session start. It contains session protocols, conventions, mailbox format, install checklist, key principles, and the header block manifest.

**Greenfield** seeds ship with pre-built template files. Claude renames, fills in placeholders, and replaces the seed CLAUDE.md with a thin router.

**Brownfield** retrofits fix folder naming, apply canonical headers, create missing files, and thin out CLAUDE.md. The CLAUDE-update.md self-destructs after completion.
