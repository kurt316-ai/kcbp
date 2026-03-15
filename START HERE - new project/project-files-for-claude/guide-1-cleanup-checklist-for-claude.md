# {PROJECT_NAME} — Cleanup Checklist

**Last updated:** {DDD DD MMM YYYY HHMM PT}

**Two modes:** Light (after compaction, 2–3 min) and Full (before major push, 10–15 min). Every section tagged [Light], [Full], or both. **Close is NOT a mode of this checklist** — Close is a universal sequence owned by `archimedes-files-for-claude/guide-1-session-and-autonomy-for-claude.md`. When Close runs, it calls §0 and §2–4 from this checklist autonomously, skips §1, then handles handoff, next session recommendation, and conditional git push itself.

**Natural triggers:** compaction recovery → Light. Kurt says "close"/"wrap up" → **Not this checklist.** Go to guide-1 Session Close. Kurt says "let's push"/"run the cleanup checklist" → Full.

**Design principle:** Close is fully autonomous — Kurt says "close" and walks away. Light and Full modes ask Kurt for input (§1) first, then go autonomous. §0 (Self-Check) is always autonomous across all modes.

**Section order:** §0 Self-Check → §1 Kurt Input (Light/Full only, skipped on Close) → §2 Roadmap Sync → §3 Context Preservation → §4 Mailbox Check → §4.5 Audit Feedback → [Light stops] → §5+ Full mode sections.

<!-- ARCHIMEDES HEADER END — do not edit above this line -->

---

## 0. Self-Check [Light] [Full]

Claude assesses these autonomously. No Kurt input required. Items needing human judgment get tagged `[KURT ACTION]` in the handoff note (during Close) or flagged inline (during Light/Full).

- [ ] Has anything in this session changed the cleanup checklist itself? If so, update this file first.
- [ ] Have any new concepts, conventions, or architecture decisions been added this session? If so, update the relevant docs (roadmap, CLAUDE.md, etc.) so they stay current.

## 1. Kurt Input [Light] [Full] — REQUIRES KURT

**This section runs during Light and Full cleanup only. Close skips it entirely.** Kurt's responsibility: share lessons learned and feedback *before* saying "close." Once the close trigger fires, Claude runs autonomously from §0 onward.

- [ ] "Did anything happen this session worth capturing in lessons-learned?" (e.g., a pattern that worked well, a mistake to avoid, a workflow improvement)
- [ ] If yes, append to `{project}-files-for-claude/capture-2-lessons-learned-for-kurt-and-claude.md` with a date stamp (create this file if it doesn't exist yet)
- [ ] If the lesson is something Archimedes should act on, also append an entry to `archimedes-mailbox/outbox.md` with status `unread`
- [ ] "Anything else I should know before I run the rest of the checklist?"

**After Kurt responds, explicitly announce:** "Going autonomous now — I'll come back with a summary and push block. You can walk away." Then run Sections 0, 2+ without further questions.

---

## 2. Roadmap Sync [Light] [Full]

**First autonomous step — update the source of truth before validating anything else.**

- [ ] All completed work is marked `done` in the phases
- [ ] No tasks are marked complete that aren't actually done
- [ ] Open questions list is current (resolved questions removed or answered)
- [ ] Decision Log includes all decisions from this session
- [ ] Version number and date are updated

## 3. Context Preservation Check [Light] [Full]

**Most critical after compaction.** Verify these facts are written in files, not lost in conversation.

- [ ] All decisions made this session are captured in the roadmap's Decision Log
- [ ] Any new conventions or patterns are documented (not just discussed)
- [ ] Project vision and end product description (in roadmap)
- [ ] Key constraints and preferences are recorded
- [ ] A new Claude session with zero context could read this folder and be productive immediately

## 4. Archimedes Mailbox Check [Light] [Full]

- [ ] Check `archimedes-mailbox/inbox.md` for entries with status `unread`
- [ ] For each unread entry: read it, take the required action, update status to `actioned`
- [ ] Check `archimedes-mailbox/outbox.md` — verify any pending entries have been written

### 4.5 Audit Feedback Check [Light] [Full]

- [ ] Check `{project}-files-for-claude/` for any `capture-*-audit-findings-*` files not yet addressed
- [ ] If new findings exist: read them, address Critical items immediately, add Important items to roadmap, batch Minor items for cleanup
- [ ] For items tagged `[KURT ACTION]`: surface to Kurt before proceeding

**Light mode stops here.** Everything below is Full mode only.

---

## 5. File Inventory [Full]

```
{PROJECT_NAME}/
├── CLAUDE.md                                          ← Router (local only)
├── {project}-overview-for-kurt.md                     ← Kurt's orientation file
├── {project}-files-for-claude/                        ← Workshop (flat, type-prefixed)
│   ├── design-1-roadmap-for-claude.md
│   ├── guide-1-cleanup-checklist-for-claude.md        ← This file
│   ├── ref-1-glossary-for-claude.md
│   ├── capture-1-idea-bin-for-kurt-and-claude.md
│   └── (more files as needed)
├── archimedes-files-for-claude/                       ← Archimedes push (read-only)
└── archimedes-mailbox/                                ← Cross-project coordination
    ├── inbox.md
    └── outbox.md
```

- [ ] All files present and in the correct folders
- [ ] No orphaned files at root level
- [ ] No duplicate files across folders

## 6. Naming Conventions [Full]

**`{project}-files-for-claude/` pattern:** `[type]-[seq]-[topic]-for-[audience].md`

- Type prefixes: `design-`, `guide-`, `ref-`, `module-`, `capture-`, `research-`
- Audience tags: `for-kurt`, `for-claude`, `for-kurt-and-claude`, `for-archimedes`
- **No version numbers.** Git tracks versions for all files.

**Root pattern:** `[project]-[topic]-for-[audience].md`

**Exemptions:** `CLAUDE.md`, `README.md`, `SKILL.md`, `inbox.md`, `outbox.md`

- [ ] All `{project}-files-for-claude/` files follow the type-prefix pattern
- [ ] Sequence numbers are assigned and in logical order within each type
- [ ] Every file has an audience tag
- [ ] No version numbers in any filenames
- [ ] No spaces in filenames

## 7. Writing Style by Audience [Full]

- `for-claude` — Technical. Concise. Structured. Every word earns its place.
- `for-kurt` — Conversational. Plain English.
- `for-kurt-and-claude` — Structured content Claude can act on, readable by Kurt.
- `for-archimedes` — Same as `for-claude`. Signals this file feeds back into Archimedes.

Checks:
- [ ] Each file's writing style matches its audience tag
- [ ] `for-claude` files have no unnecessary prose
- [ ] `for-kurt` files are readable without technical context

## 8. Stale Content Check [Full]

- [ ] No references to old filenames that don't exist on disk
- [ ] No references to old folder names
- [ ] Internal file references point to current filenames
- [ ] No outdated terminology or working names that have been replaced
- [ ] **Propagation sync:** For any source-of-truth file with a "Propagation Targets" table, verify downstream copies match the source. Fix any drift.
- [ ] No descriptions that contradict current decisions
- [ ] Headers and titles inside files match the file's current name and purpose
- [ ] All `Last updated` timestamps use Kurt's format: `DDD DD MMM YYYY HHMM PT`

## 9. Archimedes Mailbox — Outbound Check [Full]

Before pushing, check if anything from this session should be reported to Archimedes.

- [ ] Did this session discover a new pattern, anti-pattern, or tool insight not already captured in Section 1?
- [ ] Did this session hit a convention conflict or a gap in Archimedes guidance?
- [ ] Did Kurt state a preference or correction that should propagate to other projects?
- [ ] For each "yes": append an entry to `archimedes-mailbox/outbox.md` with status `unread`

## 10. Pre-Push Security Check [Full]

**BEFORE EVERY `git push` TO PUBLIC REPOS.**

Quick checks:
- [ ] Search for family names: Erika, Isabel, Ian, Dane
- [ ] Search for home nicknames: Burrow, Fawn Creek, Staunton, Coldwater
- [ ] Search for Kurt's email addresses: kurtoutdoors316, kschwarz@northslopetech, entertheforge
- [ ] Search for phone numbers and financial figures
- [ ] `.env`, `.gitignore`, `CLAUDE.md` are excluded from repo
- [ ] No `{project}-files-for-claude/` files in `output/` folder
- [ ] No root overview with PII committed to public repo

## 11. GitHub Repo Health [Full]

- [ ] Does this project have a GitHub repo? If not, and there are 3+ files, create one.
- [ ] Are there uncommitted changes? If so, commit and push.
- [ ] Does the remote match the local state?
- [ ] **One push block.** All repos, all commands, one code fence.

## 12. Folder Structure Check [Full]

- [ ] CLAUDE.md is at the parent level, not inside either subfolder
- [ ] `{project}-files-for-claude/` is flat (no subfolders)
- [ ] `archimedes-mailbox/` has inbox.md and outbox.md
