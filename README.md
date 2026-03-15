# Archimedes — Best Practices for Kurt & Claude

Conventions and infrastructure for all of Kurt's Cowork projects. Archimedes evolves best practices, pushes them to every project, and absorbs lessons learned back — so problems get solved once.

---

## START HERE

**New project (no CLAUDE.md yet):**
1. Create a project folder on your desktop
2. Copy the `CLAUDE.md` from `START HERE - no CLAUDE.md yet/` into it
3. Open Cowork, point it at the folder — Claude takes it from there

**Existing project (adding Archimedes):**
1. Copy `CLAUDE-update.md` from `START HERE - already have CLAUDE.md/` into your project folder
2. Open Cowork and tell Claude: "Read CLAUDE-update.md and follow the instructions"

---

## What's in this repo

```
archimedes/
├── archimedes-files-for-claude/       ← Distribution folder — what projects pull
├── START HERE - no CLAUDE.md yet/     ← Greenfield install seed
├── START HERE - already have CLAUDE.md/  ← Brownfield retrofit instructions
└── README.md                          ← You are here
```

**`archimedes-files-for-claude/`** is the canonical distribution folder. Every Archimedes project copies this folder locally and reads it at session start. It contains session protocols, conventions, mailbox format, install checklist, key principles, and the header block manifest.

The builder material (guides, templates, modules) lives in the local Archimedes project folder, not in this repo. This repo is the distribution channel — what projects pull from.
