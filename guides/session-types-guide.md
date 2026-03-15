# Session Types Guide

**Purpose:** Defines the seven session types across two pipelines. Every session starts by identifying its type — this keeps work focused and produces clean handoffs.
**When to Load:** Start of any session (type identification), or when session drift is detected.
**Audience:** `for-claude` — Claude identifies the session type at open and enforces discipline throughout.
**Last updated:** Sat 14 Mar 2026
**Companion docs:** `session-discipline-guide.md` (session workflow, context budget), `operational-cycle-guide.md` (maintenance cadences), `pipelines-and-routines-guide.md` (pipeline orchestration, routine inventory, documents-per-pipeline)

**Touchstone trace:** Precedes all gates — you can't evaluate safety, effectiveness, or efficiency until you know what kind of session you're in. Type identification is Gate 2 (effectiveness): wrong session type → wrong output → wasted context budget.

**Frontrunner principle:** This framework represents our best current thinking. We commit to it, run with it, and update when we learn more.

---

## Two Pipelines

**Build pipeline** — making things. Four stages that flow in sequence:

1. **Explore** → 2. **Design** → 3. **Build** → 4. **Verify**

**Thoughts & commitments pipeline** — managing things (GTD-inspired). Three stages:

1. **Capture** → 2. **Organize** → 3. **Review**

The thoughts & commitments pipeline feeds the build pipeline. Capture catches raw input. Organize routes it to projects and prioritizes. Review confirms priorities are current. Then a specific item enters the build pipeline: Explore the problem, Design the solution, Build it, Verify it works.

---

## The Seven Types

### Build Pipeline

#### 1. Explore

**Purpose:** Define the problem. Research, diagnose, investigate, discuss. Pull information in until the problem is clear.

**Output:** A clear problem statement with purpose and goal. Answers "what do we need and why."

**Aliases:** research, diagnose, investigate, discovery

**Primary tool:** Chat (Opus)

**Touchstone connection:** Precedes all gates — you can't evaluate safety, effectiveness, or efficiency until you know what you're solving.

**Open:** State the area to explore. Consume any prior handoff notes.

**Close:** Problem statement is written down (file, not conversation). Handoff note recommends Design session with pointer to the problem statement.

**Key discipline:** Don't solution yet. Resist the urge to jump to "how" — stay in "what" and "why."

---

#### 2. Design

**Purpose:** Design the solution. Architecture, approach selection, trade-off decisions. Produces a build-ready plan. This is the collaborative half of "Design then Build."

**Output:** A build brief — architecture decisions, approach, subtask decomposition, "done" criteria. Answers "how do we solve it."

**Aliases:** architect, plan, spec

**Primary tool:** Chat (Opus, collaborative)

**Touchstone connection:** Where safety and security gates get designed in, not bolted on.

**Open:** Consume the Explore output (problem statement). State the solution space to evaluate.

**Close:** Build brief written to roadmap or checkpoint file. Handoff note recommends Build session with pointer to the brief.

**Key discipline:**
- Don't start building during design — context becomes dead weight during implementation.
- Use the "Interview Me" technique for non-trivial features: "Interview me about this before planning."
- The build brief is Design's exit artifact — architecture + ordered subtasks + done criteria.
- The `[Fresh]` boundary between Design and Build is **the default for non-trivial work.** Planning context is dead weight during implementation. Skip only if Design consumed minimal context (~under 15 exchanges).

---

#### 3. Build

**Purpose:** Execute the plan autonomously. Consumes a reviewed plan, produces working output.

**Output:** Working code, docs, configuration — whatever the plan called for.

**Aliases:** implement, execute, ship

**Primary tool:** Cowork or Claude Code (Opus, autonomous) or Cowork (Sonnet, pair build)

**Touchstone connection:** Effectiveness gate — does the output match the plan?

**Open:** Consume the build brief. Front-load file reads. Confirm scope.

**Close:** Structured completion block (status, changes, verification, open items). Handoff note recommends Verify session.

**Key discipline:**
- **Autonomous mode:** Front-load reads, then stop asking. Checkpoint every 30 min. Don't redesign mid-build — capture concerns in the handoff note for a Design session.
- **Pair mode:** Keep context lean. Short responses. Test fast, fail fast. Save frequently.

---

#### 4. Verify

**Purpose:** Test and validate what was built. Stress testing, quality control, the effectiveness check.

**Output:** Binary — passes, or produces a defect list.

**Aliases:** test, audit, QA, validate, check

**Primary tool:** Cowork (Sonnet, pair build) or Claude Code

**Touchstone connection:** Effectiveness gate — formal confirmation. "Does it work?" gets a definitive answer.

**Open:** Load build output with fresh eyes. Do NOT load build conversation or planning context — the point is fresh perspective.

**Close:** Pass → handoff note for next feature (Explore or Design). Fail → defect list with severity, handoff note recommends Build session to fix.

**Key discipline:**
- Read code directly, not summaries.
- Use adversarial framing: "What's wrong?" not "Looks okay?"
- Can run as a subagent for isolated fresh context.

---

### Thoughts & Commitments Pipeline

#### 5. Capture

**Purpose:** Get raw ideas, thoughts, obligations, and commitments out of Kurt's head and into a file. Claude facilitates lightly — clarifying questions, basic grouping — but Kurt does most of the talking.

**Output:** Raw capture file. Routed into the idea bin pipeline (see `idea-bin-synthesis-guide.md`).

**Aliases:** brain dump, collect, dump, raw capture

**Primary tool:** Chat (Opus) or voice

**Touchstone connection:** Gate 2 precondition — effectiveness requires knowing what needs to be done. Capture is the intake valve.

**Open:** Kurt signals "brain dump" or "I need to get some things out of my head." Claude opens a capture file and facilitates.

**Close:** Capture file saved. Claude prompts: *"Want to run the idea bin pipeline on this, or just park it for now?"* Handoff note points to the capture file and recommends Organize if material is ready.

**Key discipline:** Don't organize yet. Don't evaluate yet. Just get it out. The only structuring allowed is light grouping to help Kurt keep talking.

---

#### 6. Organize

**Purpose:** Process captured material. Route ideas to the right project, update roadmaps, prioritize, sequence. This is a core Marvin activity — intelligent routing across all projects.

**Output:** Updated roadmaps, overview docs, or idea bin items promoted to project backlogs.

**Aliases:** process, route, prioritize, triage, roadmap update

**Primary tool:** Chat (Opus) or Cowork

**Touchstone connection:** Efficiency gate — are we working on what matters most?

**Open:** Load capture file(s) and current roadmaps for affected projects.

**Close:** All captured items are either routed to a project, parked with rationale, or discarded. Updated roadmaps reflect new priorities. Handoff note summarizes what changed.

**Key discipline:**
- Every item gets a disposition: routed, parked, or discarded.
- Routing means it appears in a specific project's roadmap or backlog — not just "noted."
- This is where the idea bin pipeline's synthesis step lives (brain dump → overview + roadmap updates).

---

#### 7. Review

**Purpose:** Reflect on commitments, priorities, and status. Are the right things being worked on? Is anything falling through the cracks? Surfaces items at the correct time.

**Output:** Updated status, reprioritized items, identified gaps.

**Aliases:** reflect, check-in, status review, weekly review

**Primary tool:** Cowork (needs artifact access) or Chat (if artifacts are uploaded)

**Touchstone connection:** All three gates — safety (nothing dangerous slipping through), effectiveness (right priorities), efficiency (no wasted effort).

**Open:** Load current roadmaps and status across active projects.

**Close:** Priorities confirmed or updated. Gaps identified with next actions. Handoff note captures any items that need Explore, Design, or Organize sessions.

**Key discipline:**
- Review ≠ Verify. **Verify** asks "does this work?" (quality gate against a specific build). **Review** asks "am I focused on the right things?" (prioritization hygiene across all commitments).
- Review surfaces work for the build pipeline. It doesn't do the work.

---

## Session Protocol

### Open Checklist (all types)

1. **Identify the session type.** Claude states it or asks. One sentence.
2. **Consume the handoff note** if one exists from a prior session.
3. **Confirm the single goal** for this session.

### Close Checklist (all types)

1. **Summarize** what was accomplished.
2. **Write the handoff note** for the next session (file, not conversation).
3. **Recommend the next session type** with rationale.

### Drift Detection

If the session drifts to a different type, Claude notes it once: *"This feels like it's shifting from Build into Design territory — want to capture this thread for a separate session?"* Then respects the answer. One nudge, not a gate.

### Handoff Notes

The handoff note is the connective tissue that makes "start fresh and start often" work. Nothing critical lives in Claude's context — it lives in the note. Handoff notes bridge sessions and bridge tools (Chat → Cowork, Cowork → Chat).

---

## Choosing a Session Type

| Situation | Session type | Why |
|-----------|-------------|-----|
| New problem, unclear requirements | Explore | Need to understand before designing |
| Problem clear, need a solution approach | Design | Architecture and tradeoffs |
| Build brief exists, scope is clear | Build (autonomous) | Execute, don't re-discuss |
| Small fix, quick iteration | Build (pair) | Overhead of design session not worth it |
| Large change set just landed | Verify | Fresh eyes catch what builders miss |
| Kurt needs to get ideas out of his head | Capture | Just get it out — don't organize yet |
| Capture file ready, need to route items | Organize | Turn raw input into project work |
| Weekly check-in, priority review | Review | Are we working on the right things? |
| Bug report, need to investigate | Explore → Build | Investigate first, then fix |

---

## Cross-References

- `session-discipline-guide.md` — session workflow, context budget, verification patterns, autonomous build protocol
- `operational-cycle-guide.md` — maintenance cadences, cleanup conventions, push protocols
- `idea-bin-synthesis-guide.md` — the synthesis process that Capture feeds into and Organize executes
- Roadmap template — What's Next queue drives session priorities
- `handoff-protocol-template.md` — handoff note structure
