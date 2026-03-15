# Session Discipline Guide

**Purpose:** Session workflow, context budget management, conversation hygiene, verification patterns, and end-of-session protocol.
**When to Load:** Start of any session (for orientation), or when session quality degrades (red flags, context issues).
**Audience:** `for-claude`
**Last updated:** Sat 14 Mar 2026
**Source:** Incorporates patterns from [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices)

**Touchstone trace:** Gate 2 (session produces correct output — context budget, verification, handoff fidelity) + Gate 3 (session is efficient — lean loading, autonomous windows, minimal Kurt interruptions). Gate 1 check: push protocols enforce security gate before code leaves the session.

---

## Principle

A Cowork session has a fixed context budget. Every file read, every conversation turn, every tool call consumes budget. When it runs out, compaction happens — and compaction always loses something. Session discipline is about spending budget on work that matters and avoiding waste that accelerates compaction.

---

## Verification: The Highest-Leverage Habit

**Rule:** If you can't verify it, flag it. Never ship unverified work.

Build verification into every task:

| Strategy | Example |
|----------|---------|
| **Success criteria** | "Test: user@example.com → true, invalid → false. Run tests after implementing." |
| **Visual verification** | "Take screenshot, compare to spec. List differences." |
| **Root cause, not suppression** | "Build fails with [error]. Fix the cause, verify build passes. Run the test." |

**`[KURT ACTION]` convention:** Tag items needing human judgment with `[KURT ACTION]` in any file. Use in findings, decisions, roadmap notes, checkpoints — anything requiring Kurt's eyes before proceeding.

**In Cowork:** Use subagents for adversarial review — fresh context catches builder bias.

---

## Session Types

**Full reference:** `session-types-guide.md` — defines all seven types, open/close protocols, and the chooser table.

**Summary:** Seven session types across two pipelines.

**Build pipeline** (making things): **Explore** → **Design** → **Build** → **Verify**

**Thoughts & commitments pipeline** (managing things): **Capture** → **Organize** → **Review**

The thoughts & commitments pipeline feeds the build pipeline. Capture catches raw input. Organize routes it. Review confirms priorities. Then items enter the build pipeline.

### Session Open (all types)

1. **Identify the session type.** Claude states it or asks. One sentence.
2. **Consume the handoff note** if one exists.
3. **Confirm the single goal.**

### Session Close (all types)

1. **Summarize** what was accomplished.
2. **Write the handoff note** (file, not conversation).
3. **Recommend the next session type** with rationale.

### The `[Fresh]` Boundary

Fresh session between Design and Build is **the default for non-trivial work**. Design context is dead weight during implementation. Skip only if Design consumed minimal context (~under 15 exchanges).

### Drift Detection

If the session drifts to a different type, Claude notes it once: *"This feels like it's shifting from Build into Design territory — want to capture this thread for a separate session?"* Then respects the answer. One nudge, not a gate.

---

## Session Start

1. Read CLAUDE.md (the project map)
2. **Identify the session type** — state it or ask Kurt (see `session-types-guide.md`)
3. Check for checkpoint files and handoff notes
4. Check roadmap status
5. Confirm the single goal for this session
6. Load only what the task requires

Budget: under 2 minutes.

**Folder selection:** Select the project folder (not parent CCF). CLAUDE.md loads automatically — you're oriented in ~2 min.

---

## Context Budget

**Expensive:** Files, long turns, tool calls, errors, unneeded reads.
**Cheap:** Short responses, targeted sections, file references, direct questions.

**Rules:**
- Read on demand, not at startup
- Use line offsets for files > 200 lines
- Don't repeat file contents ("I see the roadmap says X" wastes tokens)
- Avoid exploratory `ls`/`cat` — use CLAUDE.md routing
- New topic → new session (topic shift signals context drift)
- Copy-pasting is an automation signal — build a skill, template, or convention to replace it

**The 50% ceiling:** Past ~50% utilization, quality degrades. Model confidence stays high; accuracy drops. Watch red flags below and act proactively.

**Claude Code specifics:**
- `/compact [description]` steers what survives compaction
- `/rewind` (Esc+Esc) reverts within-session changes
- `/btw` for quick side questions (dismissible overlay)

---

## Checkpoints

**Write when:** Building 30+ min, conversation accumulated, Kurt stepping away, 100+ turns.

**Skip when:** Simple task, context already in files, recent checkpoint exists.

Checkpoints are disposable — delete after use.

---

## Autonomous Build Protocol

Build brief → execute → completion block. Three phases: entry, during, exit.

**Entry:** Write 5–15 line brief:
- What's being built (one sentence)
- Files to modify
- "Done" criteria (observable)
- Known risks
- Estimated scope (small/medium/large)

Live in roadmap's Active Item Detail (small/medium) or checkpoint file (large).

**During:** Checkpoint every 30 min. Update brief with progress. If context nears 40% and work remains, start fresh session from checkpoint. If stuck on open question, make best judgment, note `[KURT ACTION]`, keep building.

**Exit:** Structured completion block (status, changes, verification, open items, `[KURT ACTION]` if any). Goes into roadmap replacing brief, then push block.

**Break into sub-sessions if:** 5+ subtasks, large scope (45+ min), context past 40%, or 3+ `[KURT ACTION]` items.

---

## Lessons Learned

**Capture immediately:** Decision affecting project, convention going forward, gotcha for next session.

**Capture at end:** Observations on what worked, cross-project patterns (tag `for-archimedes`), Archimedes improvements.

**Skip during rapid iteration** (Pair Build). Save for end — stopping breaks flow.

---

## Conversation Hygiene

**NACK-based flow** — assume action, stop only on objection.
- Obvious (cleanup, typo, date) → do silently
- Clear (restructure file) → state as you do it, not a question
- Ambiguous/risky (delete, new arch) → "I'll do this unless you object"

**One question at a time.** Ask the most important one.

**Don't narrate plans.** Just do it. Exception: Design → Build, announce plan before going autonomous.

**Don't apologize for compaction.** Run cleanup, recover from files, resume.

**Terminal: one copy-paste block.** Cowork has no GitHub credentials — never attempt `git push` in the VM. Always produce a terminal block for Kurt to run on his Mac.
- Within repo: chain with `&&`
- Between repos: chain with `;`
- Always `cd` to Mac path first (from CLAUDE.md Working Folder)
- Always: `rm -f .git/index.lock .git/HEAD.lock` for each repo
- Always: `git push -u origin main` (not bare `git push`)
- Use `cd ../sibling` for multi-repo, not second absolute `cd`
- Add specific files, not `git add -A`
- Never stage gitignored files (`CLAUDE.md`, `.env`)
- If deleted via `rm`, use `git add <folder>/` or `git add -u <file>`, not `git rm`

**Canonical template:**
```bash
cd ~/Desktop/Claude\ Cowork\ Folders/{Project} && rm -f .git/index.lock .git/HEAD.lock && git add {files} && git commit -m "{message}" && git push -u origin main
```

**Keep response proportional:** typo → sentence, component → plan + exec, design → paragraphs, status → bullets.

---

## Close Routine

Four steps, in order:

1. **Light cleanup** (§0–4 of checklist) — dates, stale refs, naming. ~2–3 min.
2. **Handoff note** — roadmap's Active Item Detail. Where stopped, what's next, next-session context.
3. **Recommended next session type** — one of the seven types (see `session-types-guide.md`).
4. **Push check** — single copy-paste terminal block if changes exist, else skip. **Always produce this block** — Cowork cannot push directly.

**Recommended next:**

| Current state | Next | Why |
|---|---|---|
| New problem, unclear requirements | Explore | Need to understand before designing |
| Problem clear, need solution approach | Design | Architecture and tradeoffs |
| Design done, clear scope | Build | Execute from brief |
| Build done | Verify | Fresh eyes catch builder bias |
| Verify found issues | Build | Fix defects |
| Kurt has ideas piling up | Capture | Get it out of his head |
| Capture file ready | Organize | Route to projects |
| Weekly check-in due | Review | Priority hygiene |
| Everything clean | Explore | Next problem |

Format: `**Recommended next session:** [Type] — [reason]`

Kurt may override. Recommendation keeps work cycle visible.

---

## Red Flags

**Budget waste** (fix and continue):
- Re-reading recent files
- Loading arch docs for naming question (use naming conventions file)
- 500-word answer to yes/no question
- Exploring folders when CLAUDE.md has map
- Asking what's answered in roadmap
- Loading "all files just in case"
- Debugging by re-reading instead of running

**Context degradation** (start fresh immediately):
- Repeating Kurt's instruction verbatim instead of acting
- Code ignores CLAUDE.md conventions
- Confidently contradicts earlier discussion or file decision
- Kurt repeating same constraint 3+ times
- Token meter past 50%
- Same test fails 3 times (context polluted with failed approaches)

---

## Extensions (Claude Code)

**Skills** (`.claude/skills/`): Auto-loaded `SKILL.md` files. Workflows and domain knowledge. Archimedes guides are already skill-shaped; consider migrating high-value ones.

**Hooks**: Auto-run scripts at workflow points (after edits, before commits). Unlike CLAUDE.md (advisory), hooks are guaranteed. For cleanup rules you'd forget → promote to hook via `/hooks` or `.claude/settings.json`.

See `claude-code-module.md` for details.

---

## Interview Me Technique

For non-trivial features: "Interview me about this before planning." Claude asks clarifying questions → dramatically better plans. Especially useful before going autonomous.
