# Roadmap Schema — Archimedes Convention

> **Audience:** for-claude
> **Owner:** Archimedes
> **Purpose:** Defines the standard roadmap structure for all Archimedes-governed projects. Roadmaps are the operational bridge between sessions — they hold the queue that drives autonomous open and the backlog that feeds ORG sessions.

---

## Schema Overview

A roadmap has two sections with different audiences and structures:

1. **Queue** — ordered list of upcoming sessions (for-claude: structured, drives routing)
2. **Backlog** — undecomposed intentions and ideas (for-kurt: conversational, conceptual)

The queue is the execution contract. The backlog is the design surface.

---

## Queue

### Structure

Each queue item has a **structured header** (for-claude) and **nested notes** (for-kurt).

```markdown
## Queue

### 1. DES — Define shared glossary schema for Archimedes–Marvin boundary
- **Status:** next
- **Handoff:** From EXP session Sat 08 Mar 2026 — identified 4 entity types that need shared definitions. See handoff note in [link or inline].
- **Done when:** Glossary schema documented, location decided, both projects can reference it.

**Kurt's notes:**
- The glossary needs to cover GTD terms, BASB terms, and entity types (projects, areas, resources, archives)
- Marvin shouldn't own definitions — Archimedes should, and Marvin imports
- Think about whether the Touchstone vocabulary belongs here too

### 2. BLD — Implement glossary as shared ref doc
- **Status:** queued
- **Handoff:** Will come from DES session above.
- **Done when:** Ref doc exists, both CLAUDE.md files reference it.

**Kurt's notes:**
- Naming convention: ref-N-topic-for-claude.md
- Probably lives in Archimedes repo, Marvin gets a pointer

### 3. VER — Validate glossary works cross-project
- **Status:** queued
- **Handoff:** Will come from BLD session above.
- **Done when:** Tested in a live Marvin session — Claude correctly resolves shared terms.
```

### Queue Item Fields

| Field | Required | Description |
|-------|----------|-------------|
| **Sequence number** | Yes | Order in queue (1 = next) |
| **Type code** | Yes | EXP, DES, BLD, VER, CAP, ORG, REV |
| **Goal** | Yes | One sentence — what "done" looks like |
| **Status** | Yes | `next` (the one to open), `queued` (in order), `active` (in progress) |
| **Handoff** | Yes | Pointer to handoff note from previous session, or "first session" |
| **Done when** | Yes | Acceptance criteria for session close |
| **Kurt's notes** | Optional | Freeform context, thinking, constraints — Kurt's texture on the work |

### Session Type Codes

| Code | Type | Pipeline | Opens with... |
|------|------|----------|---------------|
| **EXP** | Explore | Build | Divergent questions, possibility space |
| **DES** | Design | Build | Constraints, decisions to make, tradeoffs |
| **BLD** | Build | Build | Spec + scope confirmation, then execute |
| **VER** | Verify | Build | Acceptance criteria, test against done-when |
| **CAP** | Capture | Thoughts | Raw input triage — what came in, where does it go |
| **ORG** | Organize | Thoughts | Backlog triage, promote items to queue, reorder |
| **REV** | Review | Thoughts | Step back — is the system working? What needs to change? |

---

## Backlog

### Structure

Backlog items are Kurt's undecomposed intentions. They don't have type codes or structured headers — they become queue items when promoted during an ORG session.

```markdown
## Backlog

### Voice interface for Marvin
Thinking about a voice-first interaction model. Would need to figure out STT pipeline, how it routes to the right project, and whether it's a Marvin feature or a separate layer.

### Audit pipeline design
Placeholder pipeline in Archimedes. Need to flesh out what Design → Build → Schedule → Review looks like for audits. Probably starts with an EXP session to figure out what we're even auditing.

### Dobby inventory schema
Need a durable goods inventory that tracks what's at which property. Appliances, tools, furniture. Dobby domain but Archimedes conventions.
```

### Backlog Rules

1. **No type codes.** If it has a type code, it belongs in the queue.
2. **Written for Kurt.** Conversational tone, thinking out loud, rough edges welcome.
3. **Promoted in ORG sessions.** An ORG session's concrete job is to review the backlog, decompose items into sessions, and add them to the queue.
4. **No ordering obligation.** Backlog items aren't prioritized — that happens at promotion time.

---

## Autonomous Open Routing

When a Cowork session opens, Claude executes this sequence:

1. **Read the roadmap** — find the queue item with `status: next`.
2. **Load session type protocol** — branch based on the type code (see below).
3. **Consume the handoff note** — referenced in the queue item's handoff field.
4. **Confirm the single goal** — state it, confirm with Kurt, begin.

### Type-Specific Opening Moves

| Type | Opening protocol |
|------|-----------------|
| **EXP** | "We're exploring [topic]. Here's what we know so far. I'll start with divergent questions to map the space." |
| **DES** | "We're designing [thing]. Here are the constraints and open decisions. I'll walk through each decision point." |
| **BLD** | "We're building [thing]. Here's the spec from the DES session. I'll confirm scope, then execute." |
| **VER** | "We're verifying [thing]. Here are the acceptance criteria. I'll test each one." |
| **CAP** | "Capture session. Here's what came in since last time. I'll triage each item." |
| **ORG** | "Organize session. I'll review the backlog and queue. We'll promote, reorder, or archive." |
| **REV** | "Review session. Stepping back to evaluate the system. Here's what I've observed." |

---

## Autonomous Close Checklist

Every session closes with this sequence, regardless of type:

1. **Summary** — What happened this session (2–4 sentences).
2. **Handoff note** — Context the next session needs for autonomous open. Includes:
   - Key decisions made
   - Open questions or blockers
   - Artifacts created or modified
3. **Recommend next session type** — Based on where the work landed.
4. **Update the roadmap** — Mark current session complete, confirm next item, adjust queue if needed.

Step 4 is what closes the loop. If close doesn't touch the roadmap, the queue goes stale.

---

## Drift Protocol

If a session drifts from its declared type:

1. **Note it once** — "This looks like it's becoming a DES session rather than BLD."
2. **Suggest a new session** — "Want to close this as BLD and open a DES?"
3. **Respect the answer** — If Kurt says keep going, keep going. Log the drift in the close summary.

---

## Preference Stack Integration

The following should be accessible in the web preference stack (Claude Chat):

- **Session type codes** (EXP, DES, BLD, VER, CAP, ORG, REV) and their meanings
- **Current queue state** — what's next, what's active (lightweight summary)
- **Roadmap vocabulary** — queue vs. backlog distinction

The detailed protocols (opening moves, close checklist, drift handling) live in Archimedes ref docs — too heavy for web prefs.

---

## Touchstone Traceability

| Convention | Gate | Phase | Who |
|-----------|------|-------|-----|
| Queue requires type code | Effectiveness | Build | Claude |
| Handoff note required at close | Effectiveness | Build | Claude |
| Backlog promoted only in ORG | Effectiveness | Run | Kurt |
| Close updates roadmap | Effectiveness | Run | Claude |
| Drift noted, not forced | Safety | Run | Claude |
| Kurt's notes preserved verbatim | Safety | Build | Claude |
