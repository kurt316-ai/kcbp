# Session Protocols & Autonomy Rules

**Source:** Archimedes canonical push. Do not edit — updates come from Archimedes.
**Audience:** `for-claude` — operational instructions for every session.

---

## Folder Ownership

**`archimedes-files-for-claude/` is read-only for project sessions.** This folder is owned by Archimedes and overwritten wholesale on each push. Never edit files in this folder. If you find errors, conflicts, or improvement opportunities, write to `archimedes-mailbox/outbox.md` instead — use type `convention-update` or `convention-conflict`.

## Session Open

1. Read project `CLAUDE.md` (thin router — project identity + routing pointers)
2. Read this folder (`archimedes-files-for-claude/`) for behavioral instructions — **read-only, do not edit**
3. Read `{project}-files-for-claude/` for project-specific context (roadmap, glossary, checklist)
4. Check `archimedes-mailbox/inbox.md` for unread entries

## After Compaction

If recovering from compaction (context was summarized), immediately run the **light** cleanup checklist (Sections 0–4). This takes 2–3 minutes and catches anything the summary may have lost.

## Session Close — Universal Sequence (Archimedes-Owned)

**Owner:** This section is the single source of truth for the Close sequence. Projects do NOT define their own Close mode — guide-1 controls the sequence. Project cleanup checklists provide Light and Full modes; Close lives here.

**Triggers:** Kurt says "close", "close session", "run close checklist", "let's wrap up", or "I'm done".

**Run these five steps in exact order — no skipping, no reordering:**

### Step 1 — Kurt Input
Run §0 (Self-Check) and §1 (Kurt Input) from the project's cleanup checklist. These require Kurt's response. After Kurt responds, announce: "Going autonomous now — I'll come back with a summary and push block. You can walk away."

### Step 2 — Light Cleanup (autonomous)
Run §2–4 from the project's cleanup checklist (Roadmap Sync, Context Preservation, Mailbox Check). These are the same sections that run in Light mode. Execute autonomously — no questions.

### Step 3 — Handoff Note (autonomous)
Write a handoff note in the roadmap's Active Item Detail section. Include: what was accomplished this session, what remains, any blockers or open questions.

### Step 4 — Next Session Recommendation (autonomous)
Recommend one of seven session types: Explore, Design, Build, Verify, Capture, Organize, Review. Write the recommendation into the handoff note with a one-line rationale.

### Step 5 — Paired Git Push (autonomous, mandatory)
See Paired Push Rule below. This step is mandatory if any file changed this session. Present ONE copy-paste push block — all repos, all commands, one code fence, chained with `&&`. If no files changed, state "Both repos clean — no push needed" after actually running `git status`.

**This is the default session-end.** Full cleanup (all sections of the project checklist) is for major milestones or pre-push with many changes — not for routine close.

## Paired Push Rule (Every Project)

Every project folder contains exactly two git repos. Together they are **MECE** (Mutually Exclusive, Collectively Exhaustive) — every tracked file belongs to exactly one repo, no gaps, no overlap.

**Archimedes repos:**
- **Builder** (private, `archimedes-builder`) — root `.git`. Tracks `archimedes-builder-files-for-claude/`, `archimedes-files-for-claude/`, `archimedes-mailbox/`, root Kurt-facing docs.
- **Product** (public, `archimedes`) — `output/.git`. Tracks all published output files.

**All other projects** follow the same pattern: `{project}-builder` repo + `{project}` product repo. The dividing line varies per project, but the principle is identical.

**Session-close behavior:**
1. Run `git status` in **both** repos.
2. If either has changes: stage, commit, and push.
3. Present **one** copy-paste push block chaining both repos with `&&`. Never split across multiple code fences.
4. If neither has changes: state "Both repos clean — no push needed" after actually running `git status`. Never skip the check.

**The session is not clean until both repos show no uncommitted changes and no unpushed commits.** Cowork made the changes, Cowork pushes them.

## Autonomy Rules

Anything prescribed by Archimedes conventions is pre-authorized. Do not pause to ask permission for:

- Updating file paths, dates, or headers to match current state
- Running the cleanup checklist (light or full)
- Fixing naming convention violations
- Updating the roadmap with decisions made in conversation
- Any other housekeeping defined in the project's own docs

**Default to action (NACK, not ACK).** When Kurt makes a suggestion, discuss it (including pushback), then make the change. Never ask "want me to...?", "should I...?", or "shall I go ahead?" for anything covered by existing conventions. Three tiers: (1) **Obvious** — just do it silently. (2) **Clear but non-trivial** — state what you're doing as you do it: "Adding this to the guide." Not a question. (3) **Ambiguous or high-risk** — NACK statement: "I'll make these changes unless you tell me otherwise." ACK is only appropriate when you genuinely don't know whether the action is wanted.

**Don't narrate your plan — just do it.** Exception: before going autonomous in Design then Build, summarize the build plan.

**Going autonomous: announce it.** When transitioning from interactive to autonomous work (cleanup checklist, build phase, etc.), tell Kurt: "Going autonomous now — I'll come back with [deliverable]. You can walk away."

**Grow the autonomous build window.** Every session should leave docs more complete so the next session can take on more autonomously. Document SOPs, principles, and decision patterns continuously. Surface to Kurt only when: new precedent, unclear safety gate, undocumented preference, or ambiguous domain boundary. Everything else — act.

**Terminal commands: always `cd` first.** Start every terminal block with `cd` to the project's Mac path (from CLAUDE.md `## Working Folder`). Kurt closes terminals between uses — never assume the shell is in the right directory. For push blocks, also `rm -f .git/index.lock .git/HEAD.lock` before git operations.

**When to ask:** New architecture decisions, deleting files, writing to other project folders outside mailboxes, anything not covered by an existing convention.

**`[KURT ACTION]` tag:** When writing findings, decisions, or recommendations to any file, tag items that need human judgment with `[KURT ACTION]`. This flags items Claude cannot resolve autonomously.
