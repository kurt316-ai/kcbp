# Archimedes Install Checklist

**Source:** Archimedes canonical push. Do not edit — updates come from Archimedes.
**Audience:** `for-claude` — run this after receiving an Archimedes push to verify the project is correctly set up.
**When to run:** After any `archimedes-files-for-claude/` push lands, or when Kurt asks to verify the install.

---

## How to Use

Run each check in order. Mark pass/fail. If anything fails, fix it before proceeding. Report results to Kurt at the end.

---

## §1 — Folder Structure

- [ ] `CLAUDE.md` exists at project root
- [ ] `archimedes-files-for-claude/` exists and contains files from this push
- [ ] `{project}-files-for-claude/` exists (project-specific files)
- [ ] `archimedes-mailbox/` exists with `inbox.md` and `outbox.md`
- [ ] `{project}-overview-for-kurt.md` exists at root (or is planned)

## §2 — CLAUDE.md is Thin

- [ ] CLAUDE.md contains project identity (what the project is, one paragraph)
- [ ] CLAUDE.md points to `archimedes-files-for-claude/` for behavioral instructions
- [ ] CLAUDE.md points to `{project}-files-for-claude/` for project-specific context
- [ ] CLAUDE.md has a task routing table
- [ ] CLAUDE.md does NOT duplicate behavioral content from `archimedes-files-for-claude/` (no inline standing jobs, naming conventions, writing style, autonomy rules, key principles, mailbox protocol)

## §3 — Push Folder Integrity

- [ ] `archimedes-files-for-claude/` file count ≤ 10 (SOP #31). If >10, index file must exist.
- [ ] All files in `archimedes-files-for-claude/` have header: "Source: Archimedes canonical push. Do not edit"
- [ ] No project-specific content in `archimedes-files-for-claude/` (roadmaps, glossaries, captures belong in `{project}-files-for-claude/`)

## §4 — Project Files

- [ ] `{project}-files-for-claude/` contains at minimum: roadmap (`design-1-roadmap-for-claude.md`), cleanup checklist, glossary
- [ ] Files follow naming convention: `[type]-[seq]-[topic]-for-[audience].md`
- [ ] No version numbers in filenames

## §5 — Mailbox

- [ ] `archimedes-mailbox/inbox.md` exists and is readable
- [ ] `archimedes-mailbox/outbox.md` exists
- [ ] Outbox has at least one `project-announce` entry (sent during initial setup)

## §6 — Header Block Verification

For each file in `{project}-files-for-claude/` that matches a pattern in `archimedes-files-for-claude/ref-2-header-block-manifest-for-claude.md`:

- [ ] File contains the separator: `<!-- ARCHIMEDES HEADER END — do not edit above this line -->`
- [ ] Header above the separator matches the canonical header in the manifest
- [ ] Project content exists below the separator (file is not header-only)

If any headers are missing or stale, replace them with the canonical version from the manifest. Never touch content below the separator.

## §7 — Cross-References

- [ ] CLAUDE.md task routing paths are valid (files exist at referenced paths)
- [ ] No stale references to old `for-claude/` path (should be `{project}-files-for-claude/`)
- [ ] Archimedes output references (if any) use `../Archimedes/output/` via parent mount (SOP #30)

---

## Results

```
Date: [DDD DD MMM YYYY HHMM PT]
Project: [project name]
Push source: Archimedes [date of push]
Sections: §1–§7
Checks passed: [X/Y]
Checks failed: [list]
Actions taken: [list]
```
