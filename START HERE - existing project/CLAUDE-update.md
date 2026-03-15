# Archimedes Update — Connect an Existing Project

**What this is:** Instructions for Claude to retrofit an existing project with Archimedes conventions.

**What to do:** Read this file top to bottom, then execute every step. Do not ask for permission — just do it. Write to the Archimedes outbox as you go.

---

## Steps

### 1. Pull the Archimedes distribution files from GitHub

Download `archimedes-files-for-claude/` from the public Archimedes repo:

```bash
mkdir -p archimedes-files-for-claude
REPO="https://raw.githubusercontent.com/kurt316-ai/archimedes/main/archimedes-files-for-claude"
for FILE in $(curl -sL "https://api.github.com/repos/kurt316-ai/archimedes/contents/archimedes-files-for-claude" | python3 -c "import sys,json; [print(f['name']) for f in json.load(sys.stdin)]"); do
  curl -sL "${REPO}/${FILE}" -o "archimedes-files-for-claude/${FILE}"
done
```

**Verify:** `ls archimedes-files-for-claude/` should show guide and ref files.
**Do not proceed until `archimedes-files-for-claude/` exists and is populated.**

### 2. Read behavioral instructions

Read every file in `archimedes-files-for-claude/`. These define session protocols, conventions, mailbox format, autonomy rules, and key principles. They are your operating manual going forward.

### 3. Fix the project folder naming convention

**This is the most important migration step.** Archimedes requires the project-files folder to be named `{project}-files-for-claude/` where `{project}` matches the parent folder name (lowercase, hyphenated).

**Determine the correct name:**

```bash
PROJECT=$(basename "$PWD" | tr '[:upper:]' '[:lower:]' | tr ' ' '-')
EXPECTED="${PROJECT}-files-for-claude"
```

**Check and fix — run this diagnostic in order:**

1. **If `for-claude/` exists** → rename to `${EXPECTED}/`
2. **If a `*-files-for-claude/` folder exists but the prefix doesn't match `$PROJECT`** → rename to `${EXPECTED}/`
3. **If no project-files folder exists at all** → create `${EXPECTED}/`

```bash
# Example rename
OLD=$(ls -d *-files-for-claude 2>/dev/null | grep -v archimedes | head -1)
if [ -n "$OLD" ] && [ "$OLD" != "$EXPECTED" ]; then
  mv "$OLD" "$EXPECTED"
  echo "Renamed: $OLD → $EXPECTED"
fi
```

**After renaming, update ALL internal cross-references:**
- CLAUDE.md task routing table paths
- File cross-references within the renamed folder
- Any references in root-level docs
- Cleanup checklist file inventory section

**Verify:** `ls -la "${EXPECTED}/"` should succeed.

### 4. Create the mailbox

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

### 5. Apply canonical headers to project files

Read the header block manifest: `archimedes-files-for-claude/ref-2-header-block-manifest-for-claude.md`

**For each file in `{project}-files-for-claude/` that matches a filename pattern in the manifest:**

1. **No separator present** → insert the canonical header at the top of the file, followed by the separator line (`<!-- ARCHIMEDES HEADER END — do not edit above this line -->`), then the existing content below
2. **Separator present but header differs** → replace everything above the separator with the canonical header
3. **Separator present and header matches** → no action needed

**Never touch content below the separator.**

Replace `{PROJECT_NAME}` in headers with the actual project name. Replace `{DDD DD MMM YYYY HHMM PT}` with the current date.

**If core files are missing entirely, create them** with the canonical header + separator + an empty content section:
- `capture-1-idea-bin-for-kurt-and-claude.md`
- `guide-1-cleanup-checklist-for-claude.md`
- `ref-1-glossary-for-claude.md`

### 6. Thin out CLAUDE.md

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

### 7. Self-assess and capture gaps

Check the project against Archimedes conventions. Write outbox entries for:
- Patterns that worked well (`new-pattern`)
- Convention conflicts found during migration (`convention-conflict`)
- Gaps or missing guidance (`question`)
- Tool learnings (`tool-insight`)

### 8. Run the install checklist

Run `archimedes-files-for-claude/guide-4-install-checklist-for-claude.md` end to end. Fix anything that fails.

### 9. Clean up

Delete this file (`CLAUDE-update.md`) — its job is done.

Report to Kurt: "Retrofit complete. Here's what passed, what's deferred, and what needs your input."

---

_This file self-destructs after retrofit. It should not exist in a completed Archimedes project._
