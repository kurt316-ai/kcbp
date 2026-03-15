# Pipelines & Routines Guide

**Purpose:** Enumerates all recurring work patterns in the Archimedes system — both human-driven pipelines (Cowork sessions) and system-driven routines (automated services). This is the operational map: what flows exist, what stages they have, and what documents they use.
**When to Load:** When understanding how work moves through the system, adding a new pipeline or routine, or during Review sessions.
**Audience:** `for-kurt-and-claude` — structured but readable. Kurt uses this to see the full picture; Claude uses it to route work correctly.
**Last updated:** Sat 14 Mar 2026 2130 PT
**Companion docs:** `session-types-guide.md` (defines the seven session types referenced here), `operational-cycle-guide.md` (maintenance cadences)

**Touchstone trace:** Gate 2 (effectiveness) — work that doesn't follow the right pipeline produces wrong or incomplete output. Gate 3 (efficiency) — pipelines encode learned sequences so we don't re-derive them each time.

---

## Two Categories of Recurring Work

1. **Pipelines** — human-driven, session-based workflows. Each step is a Cowork session with a defined session type. Kurt is in the loop at each stage.
2. **Routines** — system-driven automations. Actions are cron jobs, Railway services, or scheduled scripts. Kurt is notified, not driving.

---

## Pipelines

### Universal Session Protocol

Every session in every pipeline follows this protocol (full detail in `session-types-guide.md`):

- **Open:** ID the session type, consume the handoff note from the prior session, confirm the single goal.
- **Close:** Summarize what happened, write a handoff note for the next session, recommend the next session type.
- **On drift:** Note the drift once, suggest opening a new session of the appropriate type, respect Kurt's answer.

### Guidelines Status Ladder

Each session type's guidelines have a maturity status:

- **None** — doesn't exist yet. Automatic roadmap item.
- **Draft** — initial version exists, not battle-tested.
- **Stable** — tested across multiple sessions, trusted.

Currently, all seven session types have guidance consolidated in `session-types-guide.md`. No standalone per-type guidelines docs exist yet. This makes all entries **Draft** — the guidance exists but isn't isolated or battle-tested as standalone references.

---

### 1. Build Pipeline

**Purpose:** Take an idea from exploration through to verified, working output.

**Flow:** Explore → Design → **[Fresh boundary]** → Build → Verify

| Step | Session Type | Phase | Guidelines | Key Details |
|------|-------------|-------|-----------|-------------|
| 1 | **Explore** | Divergent | Draft | Research, brainstorm, compare approaches. No commitments yet. Output: problem statement with purpose and goal. |
| 2 | **Design** | Divergent → Convergent | Draft | Narrow options into a plan. Architecture, tradeoffs, subtask decomposition. Output: build brief clear enough to implement from. |
| — | **[Fresh boundary]** | — | — | Default break point for non-trivial work. New Cowork session starts here. Ensures Build gets a clean context with the Design handoff note, not a long conversation history. |
| 3 | **Build** | Convergent | Draft | Execute the design. Code, write, create. "Don't narrate your plan — just do it." Output: working artifact. |
| 4 | **Verify** | Convergent | Draft | Test, review, validate against the design. Fresh eyes — don't load build conversation. Output: pass, or defect list with severity. |

**Documents used:**
- `session-types-guide.md` — session type definitions and discipline for each step
- `session-discipline-guide.md` — context budget, verification patterns, autonomous build protocol
- Project roadmap (`design-1-roadmap-for-claude.md`) — drives what enters the pipeline
- Build brief / design spec — Design's exit artifact, Build's entry artifact
- `handoff-protocol-template.md` — handoff note structure between sessions

**Working modes:**
- **Design then Build** (Opus) — Design together in Chat, then Claude builds autonomously in Cowork.
- **Pair Build** (Sonnet) — Fast iterations, Kurt and Claude working together in Cowork.

---

### 2. Thoughts & Commitments Pipeline

**Purpose:** Move raw thoughts toward actionable commitments (actions and projects) or file them as reference. Rooted in GTD and BASB frameworks.

**Flow:** Capture → Organize → Review

| Step | Session Type | Phase | Guidelines | Key Details |
|------|-------------|-------|-----------|-------------|
| 1 | **Capture** | Divergent | Draft | Brain dump. Get it out of Kurt's head into a trusted format. No filtering, no organizing — just intake. Output: raw captured material. |
| 2 | **Organize** | Convergent | Draft | Sort captured material into the right containers. Apply GTD entity types. Route to appropriate project or area. Uses idea bin synthesis workflow. |
| 3 | **Review** | Convergent | Draft | Refine and validate. Are actions actually actionable? Are projects scoped correctly? Anything stale? Output: clean, current commitments. |

**Documents used:**
- `session-types-guide.md` — session type definitions
- `idea-bin-synthesis-guide.md` — the 4-step synthesis process (Scan & Summarize → Surface Questions → Synthesize Overview → Synthesize Roadmap)
- `ref-1-glossary-for-claude.md` — GTD/BASB framework definitions, entity type rules
- Project roadmaps — where organized items land after routing
- Project overview docs — updated during Organize with new context

**GTD entity rules (enforced during Organize):**
- **Action** = imperative verb + specific outcome. Markable done.
- **Project** = >1 action, next action not self-obvious. Markable done.
- **Area** = ongoing responsibility. Never done. Generates projects.

---

### 3. Routine Intake Pipeline *(placeholder — not yet built)*

**Purpose:** Define the process for adding a new automated routine to the system. From "I need a bot that does X" through to deployed, monitored, and registered.

**Flow:** Explore → Design → **[Fresh]** → Build → Verify → Register

| Step | Session Type | Phase | Guidelines | Key Details |
|------|-------------|-------|-----------|-------------|
| 1 | **Explore** | Divergent | None | Define what the routine needs to do. Research APIs, scraping targets, notification methods. Identify the platform (Railway, cron, etc.). |
| 2 | **Design** | Convergent | None | Architecture: scheduling, config (Google Sheets?), notifications (Resend?), monitoring (healthchecks.io?). Follow patterns from existing bots. |
| — | **[Fresh boundary]** | — | — | — |
| 3 | **Build** | Convergent | None | Implement the service. Deploy to Railway. Wire up monitoring. |
| 4 | **Verify** | Convergent | None | Confirm it runs on schedule, handles errors, sends notifications. |
| 5 | **Register** | Convergent | None | Add to project registry (`ref-2`), update this guide's Active Routines table, add to Marvin's visibility if applicable. |

**Documents used:**
- `ref-2-project-registry-for-claude.md` — registration target
- `capture-1-lessons-learned-for-kurt-and-claude.md` — patterns from wodify-booker, dunord-checker (TR workflow, polling postmortem)
- This guide (Active Routines table and Routine Schema below)

**Known patterns from existing bots:** Railway cron + Scrapfly scraping + Google Sheets config + Resend notifications + healthchecks.io monitoring. Shared service account infrastructure.

---

### 4. Audit Pipeline *(placeholder — not yet built)*

**Purpose:** Define how a new audit enters the system, gets implemented, and runs on a recurring cadence.

**Flow:** Design → Build → **Schedule** → Review

| Step | Session Type | Phase | Guidelines | Key Details |
|------|-------------|-------|-----------|-------------|
| 1 | **Design** | Convergent | None | Define what the audit checks, pass/fail criteria, cadence, and reporting format. |
| 2 | **Build** | Convergent | None | Implement the audit as a checklist, script, or automated check. |
| 3 | **Schedule** | — | None | Set the cadence (per-session, weekly, per-push, etc.). Wire into operational cycle or cron. |
| 4 | **Review** | Convergent | None | Run the audit, review findings, route fixes into the Build pipeline. |

**Documents used:**
- `ref-8-audit-framework-for-kurt-and-claude.md` — audit framework and existing audit definitions
- `operational-cycle-guide.md` — cadence inventory (where audit schedules live)
- `guide-1-cleanup-checklist-for-claude.md` — existing per-session audit (sections 0–12)

---

### 5. Capture & Explore Pipeline (Chat → Cowork)

**Status:** Active, lightweight
**Purpose:** Move ideas from spontaneous mobile exploration into project repos via structured desktop ingestion. Optimized for volume — handles the reality that ideas arrive faster than they can be processed.

**Tools:** iPhone Chat (capture), Desktop Cowork (ingest)
**Session types involved:** Capture, Explore → Organize

**Flow:** Capture & Explore (iPhone) → Triage (iPhone) → Ingest (Desktop) → Close (iPhone)

| Step | Where | Phase | Key Details |
|------|-------|-------|-------------|
| 1 | **Capture & Explore** (iPhone Chat) | Divergent | Open a new Chat session. Explore an idea conversationally — design thinking, brainstorming, problem definition. Session may produce a markdown artifact, or the conversation itself is the artifact. |
| 2 | **Triage** (iPhone Chat sidebar) | Judgment | Rename the chat with routing prefix: `COPY [PROJECT]: [name]`. Project code = routing destination. If multiple chats queued, add hyphen prefix (`-`) to indicate ingestion order. Kurt decides: which project owns this, what order matters, is the chat or its document the artifact. |
| 3 | **Ingest** (Desktop Cowork) | Convergent | Fresh Cowork session. Pull in chat content — full conversation, key excerpts, or markdown document. Integrate into the target project's docs, roadmap, or conventions. One chat per Cowork session (clean context). |
| 4 | **Close** (iPhone Chat sidebar) | — | Rename the chat to mark as ingested. Chat is fully handled — can be archived or left as reference. |

**Naming convention:**

| State | Chat Name Pattern | Meaning |
|---|---|---|
| Raw | `[default or descriptive name]` | Unprocessed conversation |
| Queued | `COPY [PROJECT]: [name]` | Ready for ingestion, routed to project |
| Prioritized | `-COPY [PROJECT]: [name]` | Ingest this one first |
| Done | `INGESTED: [name]` (or similar) | Fully processed |

**Constraints:**
- **Single-consumer pipeline.** Hyphen ordering and rename-as-status works because Kurt is the only person reading the sidebar. Not designed for shared workflows.
- **Phone → Desktop boundary is intentional.** Capture happens in motion (phone). Ingestion requires focused context (desktop + Cowork). The rename step is the bridge.
- **No automation yet.** All steps are manual. The `COPY [PROJECT]:` prefix is machine-parseable — future Marvin integration could automate triage-to-ingest handoff (detect prefix, queue for Cowork processing).

**Design notes:**
- The naming convention does double duty — it's both a routing label (which project) and a status tracker (prefixed → queued, ingested → done).
- There's an implicit triage judgment step between Capture and Ingest — deciding project ownership and priority. That's a real step, not just a rename.

---

### Pipelines on the Roadmap

These are anticipated but not yet defined enough for placeholder sections:

- **Cross-project sync pipeline** — how conventions propagate from Archimedes to child projects and learnings flow back via mailbox
- **Project onboarding pipeline** — greenfield vs. brownfield install sequences (partially captured in install-verification-guide)
- *(Add others as they become apparent)*

---

## Routines

### What Makes a Routine

Routines are **automated, recurring actions** that run without Kurt initiating each execution. They are owned by specific projects and executed by infrastructure (Railway cron, launchd, scheduled tasks), not Cowork sessions.

### Active Routines

| Routine | Owner Project | Platform | Cadence | Purpose | Repo |
|---------|--------------|----------|---------|---------|------|
| **wodify-booker** | Marvin (operational) | Railway cron | Hourly | Books 6 AM fitness classes for Kurt and Erika on Wodify | `kurt316-ai/wodify-booker` |
| **dunord-checker** | Standalone (completed) | Railway cron | Hourly | Checks Camp Du Nord availability, notifies on openings | `kurt316-ai/dunord-checker` |
| **weekly-report** | Weekly Report | Railway cron | Weekly | Orchestrates email report covering VRBO and mortgage rate data | `kurt316-ai/weekly-report` |

### Archived Routines

| Routine | Status | Notes |
|---------|--------|-------|
| **calendar-scrubber** | Archived | Precursor to Marvin. Google Sheets-based rule engine for calendar management. Marvin inherited its service account and architectural patterns. Historical reference only. |

### Routine Schema

Each routine should be documented with:

1. **Name** — kebab-case service name
2. **Purpose** — one sentence
3. **Owner project** — which project owns this routine
4. **Platform** — where it runs (Railway, launchd, cron, etc.)
5. **Cadence** — when and how often
6. **Inputs** — what data or credentials it needs
7. **Outputs** — what it produces (email, Sheet update, API call, notification, etc.)
8. **Monitoring** — how Kurt knows it's healthy or broken (healthchecks.io, etc.)
9. **Repo** — GitHub coordinates
10. **Overview doc** — link to the service's own documentation

**Common infrastructure pattern:** Railway cron + Scrapfly (scraping) + Google Sheets (config) + Resend (notifications) + healthchecks.io (uptime monitoring). Shared service account across projects.

---

## Open Questions

1. **Standalone per-type guidelines** — Should each session type get its own guidelines doc (graduating from Draft to Stable), or does the consolidated `session-types-guide.md` serve well enough? Current lean: consolidated is fine until a type's guidance gets complex enough to warrant its own file.
2. **Routine intake pipeline detail** — The placeholder captures the pattern from existing bots. Needs refinement when the next routine is built.
3. **Audit pipeline detail** — Needs refinement. The audit framework (`ref-8`) exists but the pipeline for creating and scheduling new audits isn't formalized.
4. **Marvin as routine orchestrator** — Should Marvin own visibility into all routines (monitoring dashboard, health checks), even ones owned by other projects? Current architecture has each routine self-monitoring via healthchecks.io.
5. **Pre-Archimedes routines** — wodify-booker, dunord-checker, and weekly-report predate Archimedes structure. Per project registry: won't retroactively restructure unless clear benefit. Should they get full Routine Schema docs anyway?
