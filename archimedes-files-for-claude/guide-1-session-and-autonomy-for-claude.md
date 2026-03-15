# Session Protocols & Autonomy Rules

**Source:** Archimedes canonical push. Do not edit — updates come from Archimedes.
**Audience:** `for-claude` — operational instructions for every session.

---

## Folder Ownership

**`archimedes-files-for-claude/` is read-only for project sessions.** This folder is owned by Archimedes and overwritten wholesale on each push. Never edit files in this folder. If you find errors, conflicts, or improvement opportunities, write to `archimedes-mailbox/outbox.md` instead — use type `convention-update` or `convention-conflict`.

## Session Open — Boot Sequence

The open protocol lives in the **Archimedes block** of each project's CLAUDE.md (section 2). That block is the boot sequence — it fires automatically when CLAUDE.md loads. The canonical template is in `ref-11-project-router-template-for-claude.md`.

**The boot sequence (steps 0–5):**

0. **Compaction gate** — if recovering from compaction, run the Recovery Checklist (§ "Recovery Checklist" below) before proceeding. Skip on fresh sessions.
1. **Identify** — determine session type. Read roadmap for handoff context. Confirm single goal with Kurt.
2. **Load protocol** — read this file (guide-1) for session rules and autonomy model. All other files load on demand via the CLAUDE.md routing table.
3. **Check mailbox** — read `archimedes-mailbox/inbox.md` for unread entries. *(Deferred — skip until mailbox service is operational.)*
4. **Close trigger** — at session end, when Kurt says "close": run the Session Close Checklist (§ "Session Close Checklist" below). Fully autonomous.
5. **Drift guard** — if work drifts from the declared session type, note it once and suggest opening a new session. One nudge, not a gate.

**Why the boot sequence lives in CLAUDE.md, not here:** CLAUDE.md is the only file guaranteed to load at session start. This file (guide-1) loads at step 2 of the boot sequence. If the open protocol lived only here, steps 0–1 would never fire. The CLAUDE.md block is the trigger; this file is the spec.

## Session Close Checklist (Archimedes-Owned)

**Owner:** This section is the single source of truth for the Session Close Checklist. Projects do NOT define their own close protocol — guide-1 controls it. The Project Health Checklist is a separate, comprehensive audit; Session Close is lightweight and self-contained.

**Triggers:** Kurt says "close", "close session", "run close checklist", "let's wrap up", or "I'm done".

**Fully autonomous.** When Kurt says "close", Claude runs all five steps without pausing for input. No questions, no confirmations. Kurt's one responsibility: share any lessons learned or feedback *before* saying "close." Once the trigger fires, Claude owns the rest.

**Run these five steps in exact order — no skipping, no reordering.**

**Performance rules (Gate 3 — Efficiency):**
- **Both CLAUDE.md files are already in context.** Do not re-read them. The close trigger goes straight to this section.
- **Batch reads.** Steps 2–4 all need the roadmap. Mailbox check also happens in Step 2. Fire all reads (roadmap, inbox.md, outbox.md) in one parallel batch.
- **Batch writes.** Steps 2–4 all write to the roadmap. Read once, apply all updates (status, decision log, date, handoff note, next session rec) in one or two edits — not three separate round-trips.
- **Parallel git status.** Step 5 checks two repos. Run both `git status` commands in parallel.

### Step 1 — Self-Assessment (autonomous)
Claude assesses these questions autonomously. Items requiring human judgment get tagged `[KURT ACTION]` in the handoff note (Step 3) — they do not block the close.

- Are all decisions from this session written to files (not just conversation)?
- Does CLAUDE.md still accurately reflect the project's current state?
- Did any new conventions or preferences emerge that need documenting?
- **Preference stack check:** Did this session change how sessions work (pipeline definitions, session types, handoff formats, artifact specs)? If yes, evaluate whether the change needs encoding in the preference stack (Surfaces 1–4) so future sessions inherit it. Tag as `[KURT ACTION]` if Surface 1 or 2 needs re-pasting.

### Step 2 — Session Sync (autonomous)
Update the project's source of truth before handing off. **Read the roadmap, inbox.md, and outbox.md in one parallel batch** — then apply updates.

- Roadmap: mark completed work `done`, update decision log with session decisions, update date.
- Context preservation: verify key facts are in files, not just conversation. A new Claude session with zero context should be able to pick up from here.
- Mailbox: check `archimedes-mailbox/inbox.md` for unread entries. Check outbox for any pending entries that should have been written this session. Fast-fail: if both are empty or unchanged, no action needed.

### Step 3 — Handoff Note (autonomous)
Write a handoff note in the roadmap's Active Item Detail section. Include: what was accomplished this session, what remains, any blockers or open questions, and any `[KURT ACTION]` items from Step 1. **Combine this edit with the Step 2 and Step 4 roadmap writes.**

### Step 4 — Next Session Recommendation (autonomous)
Recommend one of seven session types: Explore, Design, Build, Verify, Capture, Organize, Review. Write the recommendation into the handoff note with a one-line rationale and a brief description of what that session would cover. **This is part of the same roadmap edit as Steps 2–3.**

### Step 5 — Conditional Git Push (autonomous)
See Paired Push Rule below. **Run `git status` on both repos in parallel** (read-only — SOP #17) to detect changes. Then **present one copy-paste terminal block** for Kurt to run on his Mac. The block includes all `cd`, lock cleanup, `git add`, `git commit`, and `git push` commands. Claude never runs `git add`, `git commit`, or `git push` in the VM — those go in the copy-paste block only.

If no files changed in either repo, state "Both repos clean — no push needed" after actually running `git status`.

**This is the default session-end.** The Project Health Checklist is for major milestones or pre-push with many changes — not for routine close.

## Recovery Checklist (Archimedes-Owned)

**Purpose:** After compaction or context loss, verify that critical session state survived. Lightweight — ~2 minutes.

**Triggers:** Compaction recovery (automatic via boot sequence step 0). Kurt says "run recovery" or "quick check."

**Autonomous.** Claude runs this without pausing for input.

**Steps:**

1. **Roadmap sync** — All completed work marked `done`. Decision log includes all decisions from this session. Date is current.
2. **Context preservation** — All decisions are in files, not just conversation. New conventions are documented. A cold-start Claude could be productive immediately.
3. **Mailbox check** — Check `archimedes-mailbox/inbox.md` for unread entries. Verify any pending outbox entries have been written.
4. **Audit feedback** — Check `{project}-files-for-claude/` for any `capture-*-audit-findings-*` files not yet addressed. Address Critical items immediately, add Important items to roadmap.

After recovery, resume normal work. No handoff note, no push, no session recommendation — those are Close-only.

## Paired Push Rule (Every Project)

Every project folder contains exactly two git repos. Together they are **MECE** (Mutually Exclusive, Collectively Exhaustive) — every tracked file belongs to exactly one repo, no gaps, no overlap.

**Archimedes repos:**
- **Builder** (private, `archimedes-builder`) — root `.git`. Tracks `archimedes-builder-files-for-claude/`, `archimedes-files-for-claude/`, `archimedes-mailbox/`, root Kurt-facing docs.
- **Product** (public, `archimedes`) — `output/.git`. Tracks all published output files.

**All other projects** follow the same pattern: `{project}-builder` repo + `{project}` product repo. The dividing line varies per project, but the principle is identical.

**Session-close behavior:**
1. **Claude runs `git status`** in both repos inside the VM (read-only — SOP #17). This is the only git operation Claude executes.
2. If `archimedes-files-for-claude/` changed in the builder, the copy-paste block must sync the distribution copy first: `cp` changed files from root `archimedes-files-for-claude/` into `output/archimedes-files-for-claude/` before committing either repo.
3. If either repo has changes: **include** `git add`, `git commit`, and `git push` commands in the copy-paste block. Only include repos that have changes — skip clean repos.
4. Present **one** copy-paste push block — all sync commands, all repos, one code fence. Chain with `&&` within a repo; use `;` between repos (SOP #6). Never split across multiple code fences. Kurt does one copy-paste, one Enter.
5. If neither has changes: state "Both repos clean — no push needed" after actually running `git status`. Never skip the check.

**The session is not clean until both repos show no uncommitted changes and no unpushed commits.** Cowork made the changes, Kurt pushes them via the copy-paste block.

**Canonical push block template** (Archimedes two-repo example — adapt per project):

```
cd ~/Desktop/Claude\ Cowork\ Folders/Archimedes/ &&
rm -f .git/index.lock .git/HEAD.lock &&
git add -A &&
git commit -m "Session close: [summary of builder changes]" &&
git push -u origin main ;
cd ~/Desktop/Claude\ Cowork\ Folders/Archimedes/output/ &&
rm -f .git/index.lock .git/HEAD.lock &&
git add -A &&
git commit -m "Session close: [summary of product changes]" &&
git push -u origin main
```

**Rules for the block:** Start with `cd` to Mac path (SOP #16). Always `rm -f` lock files. Always `git push -u origin main` (SOP #15). Never include gitignored files in targeted `git add` — use `git add -A` only when confident `.gitignore` is correct (SOP #28). If only one repo has changes, only include that repo's commands.

## Autonomy Rules

Anything prescribed by Archimedes conventions is pre-authorized. Do not pause to ask permission for:

- Updating file paths, dates, or headers to match current state
- Running the Recovery Checklist or Project Health Checklist
- Fixing naming convention violations
- Updating the roadmap with decisions made in conversation
- Any other housekeeping defined in the project's own docs

**Default to action (NACK, not ACK).** When Kurt makes a suggestion, discuss it (including pushback), then make the change. Never ask "want me to...?", "should I...?", or "shall I go ahead?" for anything covered by existing conventions. Three tiers: (1) **Obvious** — just do it silently. (2) **Clear but non-trivial** — state what you're doing as you do it: "Adding this to the guide." Not a question. (3) **Ambiguous or high-risk** — NACK statement: "I'll make these changes unless you tell me otherwise." ACK is only appropriate when you genuinely don't know whether the action is wanted.

**Don't narrate your plan — just do it.** Exception: before going autonomous in Design then Build, summarize the build plan.

**Going autonomous: announce it.** When transitioning from interactive to autonomous work (Project Health Checklist, build phase, etc.), tell Kurt: "Going autonomous now — I'll come back with [deliverable]. You can walk away."

**Grow the autonomous build window.** Every session should leave docs more complete so the next session can take on more autonomously. Document SOPs, principles, and decision patterns continuously. Surface to Kurt only when: new precedent, unclear safety gate, undocumented preference, or ambiguous domain boundary. Everything else — act.

**Terminal commands: always `cd` first.** Start every terminal block with `cd` to the project's Mac path (from CLAUDE.md `## Working Folder`). Kurt closes terminals between uses — never assume the shell is in the right directory. For push blocks, also `rm -f .git/index.lock .git/HEAD.lock` before git operations.

**When to ask:** New architecture decisions, deleting files, writing to other project folders outside mailboxes, anything not covered by an existing convention.

**`[KURT ACTION]` tag:** When writing findings, decisions, or recommendations to any file, tag items that need human judgment with `[KURT ACTION]`. This flags items Claude cannot resolve autonomously.
