# Archimedes Operational Cycle Guide

**Purpose:** Defines when each maintenance process runs, how they chain together, and the full cadence inventory. Covers cleanup, push, compaction, reconciliation, and all recurring routines.
**Audience:** `for-claude`
**Companion doc:** `archimedes-system-guide-for-kurt.md` (project root) Part 3 has human-readable explanations.
**Prerequisite:** `session-discipline-guide.md` covers session-level behavior (context budget, workflow modes). This guide covers the system-level cycle that sits above any single session.
**Last updated:** Sat 14 Mar 2026
**Source:** Incorporates patterns from [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices)

**Touchstone trace:** Gate 2 (maintenance cycles keep the system effective — stale content, broken references, and drift are effectiveness failures) + Gate 3 (right cadence — frequent enough to catch problems, infrequent enough to not waste Kurt's time). Gate 1 check: security audit and push protocols are embedded in the cycle.

## When to Load

- After compaction recovery (to know what maintenance to run)
- Before a push (to confirm you've followed the full pre-push sequence)
- When planning session work (to know what recurring maintenance is due)
- When setting up a new project (to configure its maintenance cadences)

---

## The Session Lifecycle

Every session follows this cycle. Each step has a defined trigger.

```
Session start (or compaction recovery)
    │
    ├─ Light cleanup (2–3 min)
    │
    ├─ Work phase
    │   ├─ Checkpoint if autonomous build > 30 min
    │   ├─ Push after completing a coherent unit of work
    │   │   └─ Full cleanup runs BEFORE each push
    │   └─ Continue working
    │
    ├─ Compaction approaching (context getting heavy)
    │   ├─ Finish current unit of work if close to done
    │   ├─ Push if meaningful uncommitted work exists
    │   └─ Checkpoint if mid-task
    │
    ├─ Compaction happens
    │   └─ Return to top: light cleanup → resume
    │
    └─ Session end (Kurt says "close" or equivalent)
        ├─ 1. Light cleanup (dates, stale refs, naming drift)
        ├─ 2. Handoff note in roadmap Active Item Detail
        ├─ 3. Recommended next session type (one of 7 — see session-types-guide)
        ├─ 4. Check if push needed → build push block if yes
        └─ (Aliases: "close", "close session", "run close checklist")
```

---

## The Work Cycle

The session lifecycle (above) describes maintenance. The work cycle describes how to approach tasks across one or more sessions. **Session types are defined in `session-types-guide.md`** — seven types across two pipelines.

### Two Pipelines

**Build pipeline** — making things:

```
Explore → Design → [Fresh] → Build → Verify → Improve
```

**Thoughts & commitments pipeline** — managing things (feeds the build pipeline):

```
Capture → Organize → Review
```

The thoughts & commitments pipeline surfaces and prioritizes work. The build pipeline executes it. Capture catches raw input, Organize routes it to projects, Review confirms priorities. Then specific items enter the build pipeline.

### Build Pipeline Phases

| Phase | Session type | What happens | Key principle |
|-------|-------------|-------------|---------------|
| **Explore** | Explore session | Research, diagnose, investigate. Define the problem. | Understand before solving |
| **Design** | Design session | Architecture, tradeoffs, subtask decomposition. Produce build brief. | Think before building |
| **[Fresh]** | — | Start a new session. Design context consumed budget; execution starts clean. | Design context is dead weight during implementation |
| **Build** | Build session | Execute from the brief. Autonomous (Opus) or pair (Sonnet). | Full attention capacity on the actual work |
| **Verify** | Verify session | Fresh context reviews output. Adversarial framing. | Fresh eyes catch what builders miss |
| **Improve** | Any | Update CLAUDE.md with what worked. Capture lessons. Push. | The cycle compounds — each pass improves the next |

### Thoughts & Commitments Pipeline Phases

| Phase | Session type | What happens | Key principle |
|-------|-------------|-------------|---------------|
| **Capture** | Capture session | Brain dump. Get ideas, obligations, commitments out of Kurt's head into a file. | Don't organize yet — just get it out |
| **Organize** | Organize session | Route captured items to projects, update roadmaps, prioritize. | Every item gets a disposition: routed, parked, or discarded |
| **Review** | Review session | Reflect on commitments and priorities across all projects. | Review ≠ Verify. Review asks "right things?" not "does it work?" |

The `[Fresh]` boundary is **the default for non-trivial work**. Skip it only when Design consumed minimal context (rough threshold: under ~15 exchanges).

Not every task requires all phases. Small fixes skip Explore and Design. Well-understood features may skip Explore. The close routine evaluates where the work is and recommends the right next step.

**The "interview me" technique:** Before designing, tell Claude "Interview me about this feature." Claude asks clarifying questions that surface requirements you wouldn't have specified — producing dramatically better designs.

**Course correction during implementation:** Use `Esc` to stop Claude mid-action (context preserved, redirect). Use `Esc+Esc` or `/rewind` to restore any previous checkpoint. If you've corrected Claude more than twice on the same issue, `/clear` and start fresh with a better prompt — a clean session with a refined prompt always outperforms a cluttered one with accumulated corrections.

---

## Skills and Hooks in the Lifecycle

Two Claude Code extension mechanisms fit into the operational cycle:

### Skills (`.claude/skills/`)

Skills are `SKILL.md` files loaded on demand — domain knowledge, reusable workflows, and repeatable processes that don't consume CLAUDE.md budget. They auto-detect by relevance or invoke explicitly with `/skill-name`.

**Where skills fit:** Replace "conditional loading" patterns in CLAUDE.md routing. Instead of routing Claude to a guide file, the guide becomes a skill that Claude loads when it recognizes the task type. This reduces CLAUDE.md size and improves targeting.

### Hooks (`.claude/settings.json`)

Hooks are deterministic scripts that run at specific workflow points — after file edits, before commits, etc. Unlike CLAUDE.md rules (advisory), hooks execute every time with no exceptions.

**Where hooks fit:** Promote any cleanup checklist item that should *never* be skipped. Examples: lint after edit, naming convention validation before commit, secrets scan before push. Configure via `/hooks` or by editing `.claude/settings.json` directly.

---

## Cleanup Conventions

### Light Cleanup

**Trigger:** After every compaction recovery. Also after completing a major task mid-session.
**Time:** 2–3 minutes.
**What it covers:** Sections 0–4 of the cleanup checklist. Kurt input (0–1), then autonomous: context preservation, roadmap sync, mailbox check. "Did we lose anything?"
**Gate rule:** Do not act on the user's pending request until light cleanup is complete. The pending task will still be there after the checklist.

### Full Cleanup

**Trigger:** Before every `git push`. End of session. When Kurt says "run the cleanup checklist."
**Time:** 10–15 minutes.
**What it covers:** All sections (0–12) of the cleanup checklist. File inventory, naming, style, stale content, registry sweep, repo health.
**Output:** One copy-paste push block for all repos (chained with `&&` and `cd ../sibling`). Never split across multiple code fences.

### Close Routine

**Trigger:** Kurt says "close", "close session", "run close checklist", "let's wrap up", or "I'm done."
**Time:** 3–5 minutes.
**What it covers:** Four steps, in order:

1. **Light cleanup** — dates, stale refs, naming drift (cleanup checklist §0–4). May surface items worth noting in step 2.
2. **Handoff note** — write into roadmap Active Item Detail. Where we stopped, what's next, any context the next session needs.
3. **Recommended next session type** — evaluate where the work is across both pipelines and recommend which of the seven session types comes next. Write the recommendation into the handoff note. See `session-types-guide.md` § Choosing a Session Type.
4. **Push check** — if there are changes worth persisting, build and present the push block. If nothing meaningful changed, skip.

The close routine is the **standard way sessions end.** Full cleanup (all 12 sections) is reserved for major milestones or when Kurt explicitly asks for it. Most sessions don't need a full cleanup at close — the light cleanup + handoff + push is sufficient.

### The Relationship

Three cleanup modes, each a superset of the one before:

| Event | Cleanup mode |
|-------|-------------|
| Compaction recovery | Light (§0–4) |
| Major task completed mid-session | Light (§0–4) |
| **End of session** | **Close routine** (light + handoff + push check) |
| Before a major push with many changes | Full (§0–12) |
| Kurt says "run the checklist" | Full (unless he specifies light or close) |

---

## Push Conventions

### When to Push

A push happens when there's a **coherent unit of work** worth committing. Not after every file edit, but not only at session end either.

| Signal | Push? |
|--------|-------|
| Completed a feature, guide, or design decision set | Yes |
| Finished a conversation that produced file changes | Yes |
| About to start a task that will consume heavy context (large file reads, long builds) | Yes — push first to back up current work |
| Compaction feels imminent (context getting heavy, long session) | Yes — push to back up, then checkpoint if mid-task |
| Fixed a typo or updated a date | No — batch with next meaningful change |
| Mid-task, files are in a transitional state | No — finish the unit of work first |

### Push Sequence

Every push follows this exact order:

1. Full cleanup (sections 0–12)
2. Stage specific files (not `git add -A`)
3. Commit with descriptive message
4. Present one copy-paste push block to Kurt
5. Wait for Kurt to paste and confirm

### Pre-Compaction Push

When context is getting heavy and compaction feels likely:

1. Assess: am I close to finishing the current task?
   - If yes → finish, then push
   - If no → push current state, then checkpoint the remaining work
2. After compaction → light cleanup → resume from checkpoint or roadmap

---

## Compaction Conventions

### Before Compaction

Claude cannot predict exactly when compaction will happen, but the signals are:
- Session has been long (many turns, many file reads)
- Context feels heavy (Claude's responses becoming less precise)
- Large file operations are about to happen

**When signals appear:**
1. Finish the current atomic unit of work if possible
2. Push if there are meaningful uncommitted changes
3. Write a checkpoint if mid-task with context that only lives in conversation
4. Ensure the roadmap reflects current state

### After Compaction

1. Run light cleanup (sections 0–3) — this is a gate, not optional
2. Re-read the roadmap What's Next queue
3. Check for checkpoint files
4. Resume the pending task
5. Do NOT apologize for compaction or re-explain what happened

---

## Cadence Inventory

All recurring processes, their triggers, and their frequencies.

### Per-Session Cadences

| Process | Trigger | Frequency | Time | Reference |
|---------|---------|-----------|------|-----------|
| Light cleanup | Compaction recovery | Every compaction | 2–3 min | Cleanup checklist §0–4 |
| Close routine | End of session | Once per session | 3–5 min | This guide § Close Routine |
| Full cleanup | Before major push / Kurt asks | As needed | 10–15 min | Cleanup checklist §0–12 |
| Push | Coherent unit of work complete | 1–3× per session | 2 min | This guide § Push Conventions |
| Checkpoint | Long autonomous build / pre-compaction | As needed | 2 min | Session discipline guide |
| Lessons capture | Decisions, conventions, gotchas | Immediately when discovered | 1 min each | Session discipline guide |

### Periodic Cadences

| Process | Trigger | Frequency | Time | Reference |
|---------|---------|-----------|------|-----------|
| Reconciliation cycle | Scheduled or context bloat | Weekly | 30–60 min | Markdown architecture guide |
| Template freshness check | Part of reconciliation | Weekly (bundled) | 10 min | File type optimization guide § Template |
| Lessons harvest | Part of reconciliation | Weekly (bundled) | 15 min | Cross-project sweep of capture files |
| Token budget audit | Part of reconciliation | Weekly (bundled) | 10 min | Markdown architecture guide § Principle 3 |
| TEMP tag processing | Part of reconciliation | Weekly (bundled) | 5 min | Markdown architecture guide § TEMP convention |

### Project-Level Cadences

| Process | Trigger | Frequency | Time | Reference |
|---------|---------|-----------|------|-----------|
| Project reconciliation | Scheduled | Weekly per active project | 15–30 min | Cleanup checklist full mode |
| Archimedes mailbox check (per project) | Session start or routing trigger | Every session (if mailbox exists) | 1 min | TBD — mailbox design pending |
| Archimedes mailbox scan (all projects) | Scheduled | Weekly from Archimedes session | 10–15 min | TBD — mailbox design pending |

### Strategic Cadences

| Process | Trigger | Frequency | Time | Reference |
|---------|---------|-----------|------|-----------|
| Preferences alignment audit | Cleanup checklist §0 or scheduled | Monthly (bundled with reconciliation) | 15 min | Preferences reference file (in builder repo) — verify all 4 surfaces match |
| Toolkit research | Scheduled or new project need | Monthly | 1–2 hours | Tools research guide (TBD) |
| Official docs review | Scheduled | Monthly | 30–60 min | Docs monitor file (in builder repo) |
| Cold-read audit | Milestone or periodic | Per project, quarterly or per major milestone | 30–60 min | Separate auditor session |
| Project registry update | After project changes | As needed, verified monthly | 15 min | Project registry |

---

## Cross-References

- `session-discipline-guide.md` — session-level behavior (context budget, workflow modes, checkpoint timing)
- Cleanup checklist — the actual checklist Claude runs (this guide defines *when*, the checklist defines *what*)
- `markdown-architecture-guide.md` — reconciliation cycle details
- `file-type-optimization-guide.md` — type-specific maintenance considerations
- Roadmap template — What's Next queue drives session priorities
