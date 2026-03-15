# Archimedes Update — Connect an Existing Project

**What this is:** Instructions for Claude to retrofit an existing project with Archimedes conventions.

**What to do:** Read this file top to bottom, then execute every step. Do not ask for permission — just do it. Write to the Archimedes outbox as you go.

---

## Steps

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

Read every file in `archimedes-files-for-claude/`. These define session protocols, conventions, mailbox format, autonomy rules, and key principles. They are your operating manual going forward.

### 3. Create the mailbox

Create `archimedes-mailbox/` with `inbox.md` and `outbox.md` (if they don't already exist).

Write a `project-announce` entry to the outbox immediately:
```markdown
## Entry — {DDD DD MMM YYYY HHMM PT}
**Status:** unread
**Type:** project-announce
**Topic:** Retrofit: {project name} now on Archimedes protocols
**Content:**
- **What:** {one-line description}
- **Claude account:** {personal or Northslope}
- **GitHub:** {repo URL}
- **Mac path:** ~/Desktop/Claude Cowork Folders/{folder}/
- **Tech stack:** {tools/platforms}
- **Archimedes compliance:** Brownfield retrofit — CLAUDE-update.md applied this session.
```

### 4. Migrate project files

Rename `for-claude/` to `{project}-files-for-claude/` (if it exists under the old name). Update all internal cross-references.

For each file in `{project}-files-for-claude/` that matches a pattern in `archimedes-files-for-claude/ref-2-header-block-manifest-for-claude.md`, apply the canonical header block and separator.

If core files are missing, create them:
- **Idea bin:** `capture-1-idea-bin-for-kurt-and-claude.md`
- **Cleanup checklist:** `guide-1-cleanup-checklist-for-claude.md`
- **Glossary:** `ref-1-glossary-for-claude.md`

### 5. Thin out CLAUDE.md

Rebuild CLAUDE.md as a thin router. Move all behavioral content (standing jobs, naming conventions, writing style, autonomy rules, key principles, mailbox protocol) out — those now live in `archimedes-files-for-claude/`.

**CLAUDE.md should contain:**
- **Project identity** — one paragraph (what the project is, domain boundaries)
- **Archimedes pointer** — "Read `archimedes-files-for-claude/` for behavioral instructions. Owned by Archimedes — never edit these files. If you find errors, conflicts, or improvements, write to `archimedes-mailbox/outbox.md` instead."
- **Project files pointer** — "Read `{project}-files-for-claude/` for project-specific context."
- **Folder structure diagram**
- **Start Here** — ordered reading list
- **Task routing table** — map task types to the right files
- **Project-specific principles** — domain rules that don't belong in Archimedes (e.g., Dobby/Marvin boundary)

**Preserve** existing project-specific content (task routing, domain context). **Remove** anything now covered by `archimedes-files-for-claude/`.

### 6. Self-assess and capture gaps

Check the project against Archimedes conventions. Write outbox entries for:
- Patterns that worked well (`new-pattern`)
- Convention conflicts found during migration (`convention-conflict`)
- Gaps or missing guidance (`question`)
- Tool learnings (`tool-insight`)

### 7. Run the install checklist

Run `archimedes-files-for-claude/guide-4-install-checklist-for-claude.md` end to end. Fix anything that fails.

### 8. Clean up

Delete this file (`CLAUDE-update.md`) — its job is done.

Report to Kurt: "Retrofit complete. Here's what passed, what's deferred, and what needs your input."

---

_This file self-destructs after retrofit. It should not exist in a completed Archimedes project._
