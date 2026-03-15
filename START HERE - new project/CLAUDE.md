# Project Configuration

## Archimedes Protocols (Kurt & Claude Best Practices)

This project follows **Archimedes protocols** — a cross-project system of conventions and infrastructure for all of Kurt's Cowork projects.

**Archimedes repo:** https://github.com/kurt316-ai/archimedes

## First Session Instructions

**Do these in order. Don't skip steps.**

### 1. Rename the project folders

This seed shipped with placeholder names. Rename them now using the folder name as the project name:

```bash
# Determine project name from the folder name (lowercase, hyphenated)
PROJECT=$(basename "$PWD" | tr '[:upper:]' '[:lower:]' | tr ' ' '-')

# Rename project-files-for-claude → {project}-files-for-claude
mv project-files-for-claude "${PROJECT}-files-for-claude"
```

Then do a find-and-replace across all files in `{project}-files-for-claude/`, `archimedes-mailbox/`, and this file:
- `{PROJECT_NAME}` → the human-readable project name (e.g., "Dobby")
- `{project}` → the lowercase-hyphenated folder prefix (e.g., "dobby")
- `{DDD DD MMM YYYY HHMM PT}` → the current date in Kurt's format

### 2. Pull the Archimedes distribution files from GitHub

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

### 3. Read behavioral instructions

Read every file in `archimedes-files-for-claude/`. These define session protocols, conventions, mailbox format, autonomy rules, and key principles. They are your operating manual.

### 4. Verify the seed structure

Everything below should already exist from the seed. Confirm each item:

```
{project}/
├── CLAUDE.md                          ← This file (you'll replace it in step 5)
├── .gitignore                         ← Already seeded
├── archimedes-files-for-claude/       ← Copied in Step 2 (read-only, Archimedes owns)
├── archimedes-mailbox/
│   ├── inbox.md                       ← Already seeded
│   └── outbox.md                      ← Already seeded (write project-announce entry now)
└── {project}-files-for-claude/
    ├── capture-1-idea-bin-for-kurt-and-claude.md   ← Already seeded
    ├── guide-1-cleanup-checklist-for-claude.md     ← Already seeded
    └── ref-1-glossary-for-claude.md                ← Already seeded
```

**Action:** Write the `project-announce` entry in `archimedes-mailbox/outbox.md` now (template is in that file as a comment).

### 5. Create paired GitHub repos

The bootstrap front-loads all setup so future sessions can just build. That includes version control.

**Determine the GitHub account** from the project registry or ask Kurt:
- Personal projects → `kurt316-ai` (GitHub) / `kurtoutdoors316@gmail.com`
- Northslope projects → `kurt-ai-316` (GitHub) / `kschwarz@northslopetech.com`

**Create the repos:**

```bash
# Initialize git and make initial commit with the verified seed
git init
git add -A
git commit -m "Archimedes greenfield bootstrap — initial seed"

# Create paired GitHub repos (adjust GITHUB_USER)
GITHUB_USER="kurt316-ai"  # or "kurt-ai-316" for Northslope

# Public repo — the deliverable (if applicable)
gh repo create "${GITHUB_USER}/${PROJECT}" --public --source=. --remote=origin --push

# Private builder repo (if the project needs a separate builder workspace)
# gh repo create "${GITHUB_USER}/${PROJECT}-builder" --private --source=. --remote=origin --push
```

**Decide repo topology with Kurt:**
- **Single repo** (default for most projects) — one private repo holds everything.
- **Paired repos** (for projects with a public deliverable) — public repo for the user-facing toolkit, private `-builder` repo for workshop files. Archimedes and Cato use this pattern.

**Verify:** `git remote -v` shows the correct origin. `gh repo view` confirms the repo exists on GitHub.

### 6. Replace this file

Build a thin CLAUDE.md router:
- **Project identity** — one paragraph (what the project is, domain boundaries)
- **Archimedes pointer** — "Read `archimedes-files-for-claude/` for behavioral instructions. Owned by Archimedes — never edit these files. If you find errors, conflicts, or improvements, write to `archimedes-mailbox/outbox.md` instead."
- **Project files pointer** — "Read `{project}-files-for-claude/` for project-specific context."
- **Folder structure diagram**
- **Start Here** — ordered reading list
- **Task routing table** — map task types to the right files

Replace this seed file with the router. The seed's job is done.

### 7. Run the install checklist

Run `archimedes-files-for-claude/guide-4-install-checklist-for-claude.md` end to end. Fix anything that fails before reporting to Kurt.

### 8. Ask Kurt what's next

Setup complete. Ask Kurt one question at a time about the project — start with "What does this project do?" if no context exists yet.

---

_This is a seed file. After setup, Claude replaces it with a thin project CLAUDE.md._
