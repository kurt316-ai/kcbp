# Project Configuration

## Archimedes Protocols (Kurt & Claude Best Practices)

This project follows **Archimedes protocols** — a cross-project system of conventions and infrastructure for all of Kurt's Cowork projects.

**Archimedes repo:** https://github.com/kurt316-ai/archimedes

## First Session Instructions

**Do these in order. Don't skip steps.**

### 1. Get the Archimedes distribution files

Clone the Archimedes repo and copy the distribution folder into this project:

```bash
git clone https://github.com/kurt316-ai/archimedes.git /tmp/archimedes-ref
cp -r /tmp/archimedes-ref/archimedes-files-for-claude/ archimedes-files-for-claude/
```

If clone fails (network/auth), ask Kurt to run this on his Mac:
```bash
cd ~/Desktop/Claude\ Cowork\ Folders/{THIS_FOLDER} && git clone https://github.com/kurt316-ai/archimedes.git /tmp/archimedes-ref && cp -r /tmp/archimedes-ref/archimedes-files-for-claude/ archimedes-files-for-claude/
```
**Do not proceed until `archimedes-files-for-claude/` exists in this project.**

### 2. Read behavioral instructions

Read every file in `archimedes-files-for-claude/`. These define session protocols, conventions, mailbox format, autonomy rules, and key principles. They are your operating manual.

### 3. Set up the project structure

Create the following:

```
{project}/
├── CLAUDE.md                          ← Thin router (you'll replace this seed file)
├── archimedes-files-for-claude/       ← Already copied in Step 1 (read-only, Archimedes owns)
├── archimedes-mailbox/
│   ├── inbox.md                       ← FROM Archimedes (create empty)
│   └── outbox.md                      ← TO Archimedes (create with project-announce entry)
├── {project}-files-for-claude/
│   ├── capture-1-idea-bin-for-kurt-and-claude.md
│   ├── guide-1-cleanup-checklist-for-claude.md
│   └── ref-1-glossary-for-claude.md
└── {project}-overview-for-kurt.md     ← Created at synthesis (not now)
```

**Key setup actions:**
- Create `{project}-files-for-claude/` with idea bin, cleanup checklist, and glossary. Use the header block manifest (`archimedes-files-for-claude/ref-2-header-block-manifest-for-claude.md`) for canonical headers on each file.
- Create `archimedes-mailbox/` with `inbox.md` and `outbox.md`. Write a `project-announce` entry to the outbox immediately.
- Create `.gitignore` with standard exclusions: `CLAUDE.md`, `.env`, `.env.*`

### 4. Replace this file

Build a thin CLAUDE.md router:
- **Project identity** — one paragraph (what the project is, domain boundaries)
- **Archimedes pointer** — "Read `archimedes-files-for-claude/` for behavioral instructions. Owned by Archimedes — never edit these files. If you find errors, conflicts, or improvements, write to `archimedes-mailbox/outbox.md` instead."
- **Project files pointer** — "Read `{project}-files-for-claude/` for project-specific context."
- **Folder structure diagram**
- **Start Here** — ordered reading list
- **Task routing table** — map task types to the right files

Replace this seed file with the router. The seed's job is done.

### 5. Run the install checklist

Run `archimedes-files-for-claude/guide-4-install-checklist-for-claude.md` end to end. Fix anything that fails before reporting to Kurt.

### 6. Ask Kurt what's next

Setup complete. Ask Kurt one question at a time about the project — start with "What does this project do?" if no context exists yet.

---

_This is a seed file. After setup, Claude replaces it with a thin project CLAUDE.md._
