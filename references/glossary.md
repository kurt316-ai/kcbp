# Archimedes Glossary — Universal Terms

**Purpose:** Consistent terminology across all Archimedes-managed projects. When in doubt, check here first.
**When to Load:** When encountering unfamiliar Archimedes terminology. Also during stale content checks (cleanup checklist Section 12).
**Last updated:** Sat 14 Mar 2026
**Audience:** `for-kurt-and-claude` — structured and scannable for Claude, but includes Kurt's conceptual shorthand and conversational definitions that serve both readers.

---

## Document & Collection Types

| Term | Definition | Example |
|---|---|---|
| **Registry** | The authoritative, actively maintained record of what exists. Detailed enough to locate and describe each entry. Updated every cleanup pass. Living document. | Project registry (in `for-claude/`): one entry per project with folder, purpose, tech stack, LL version. |
| **Index** | Retired. Use **registry** when tracking things officially, or **reference** when it's a static lookup. Don't use "index" — it overlaps with registry and causes confusion. | — |
| **Library** | A collection of knowledge entries on a single theme, drawn from multiple sources. Entries accumulate over time. | Lessons learned library (in `for-claude/`): many lessons from many projects, one doc. |
| **Reference** | A static or slow-changing lookup document. Not actively maintained on a schedule — updated when the underlying facts change. | Tech stack reference, naming conventions doc, glossary (this file). |
| **Template** | A starter document with placeholders and structure that gets copied into a new project and filled in. | Roadmap template, cleanup checklist template, README template. |
| **Guide** | A how-to document. Teaches a process or set of best practices. Read, not copied. | Session discipline guide, compaction survival guide. |
| **Module** | A self-contained package of best practices for a specific tool or domain. Loaded conditionally based on what a project uses. | Notion module, Railway module, Google Sheets module. |
| **Skill** | A Cowork skill file (SKILL.md + supporting files). Executable by Claude, triggered by name or description match. | Project kickoff skill, project audit skill. |
| **Paired document** | Two files covering the same content for different audiences: a `for-claude` version (terse, structured, token-efficient) and a `for-kurt` version (readable, explanatory, includes reasoning). Aliases: **dual document**. See decision #86. | Markdown architecture guide: `markdown-architecture-guide.md` (for-claude) + `markdown-architecture-guide-for-kurt.md` (for-kurt). |

## Project Structure Terms

| Term | Definition |
|---|---|
| **CCF (Claude Cowork Folders)** | The root folder on your desktop that contains all Claude Cowork projects. Every project folder lives under CCF. Typical path: `~/Desktop/Claude Cowork Folders/`. |
| **Project parent folder** | The CCF subfolder for a project (e.g., `{your-project}/`). Contains `for-claude/`, `output/`, `archimedes-mailbox/`, and `CLAUDE.md` at root. This is the folder selected in Cowork. Standard convention for all projects. |
| **Builder (folder)** | The workshop folder (`[project]-builder/`). Has its own `.git` repo (private). Research, drafts, roadmap, cleanup checklist. Never ships. |
| **User (folder)** | The deliverable folder (`[project]/`). Has its own `.git` repo (public or private depending on project). What gets used, shipped, or consumed. |
| **Starter file** | The one file Kurt drops into a new project to bootstrap it with Archimedes. Points Claude to the repo. All intelligence lives in the repo, not the seed. |
| **Seed file** | Synonym for starter file. The 14-line file that bootstraps a new project with Archimedes. Sometimes used specifically for greenfield installs (vs. CLAUDE-update.md for brownfield/existing projects). |
| **Router README** | A project-level README or CLAUDE.md that acts as a dispatcher — routes Claude to the right docs per task type. Lightweight, not an encyclopedia. |
| **Task routing table** | A table inside a router README that maps task types to which files Claude should read (and which to skip). Includes trigger phrases. |

## Planning Terms

| Term | Definition |
|---|---|
| **Roadmap** | Strategic view of what's being built and in what order. Answers "where are we going?" Sits above projects as a manager — a roadmap may contain multiple projects or subprojects in a hierarchy. Includes components, phases, design rationale, and decision history. Changes when strategy changes. In Archimedes, every project gets one. The roadmap is the top-down view of the build. |
| **Queue (What's Next)** | A deliberately sequenced list that drives action. Answers "what's next and in what order?" More intentional than a backlog — the ordering itself is a decision. Max 7 active items. May sequence tasks within a project or sequence projects within a roadmap. Changes when priorities shift. In the Archimedes roadmap template, the "What's Next" section is a queue embedded inside the roadmap. Uses dual numbering: **Seq** (execution order, changes with reprioritization) and **ID** (permanent identifier for cross-references, never changes). |
| **Seq (Sequence number)** | Execution order in the queue. Changes whenever priorities shift. Done items use `—`. Parked items use `P`. When Kurt asks "what's next," Claude reads by Seq order. |
| **ID (Permanent identifier)** | Unique identifier assigned when a queue item is first created. Never changes, even if the item moves in priority. Used by the decision log for cross-references (e.g., "implements ID8"). Dependencies reference by ID, not Seq. |
| **Backlog** | Everything that's been identified as work but isn't prioritized into the queue. No particular order. Items get promoted into What's Next as slots open up. Not "deferred" — just not yet sequenced. |
| **Project plan** | Execution breakdown: tasks, dependencies, milestones, sequencing. Answers "how do we get from here to done?" In the Archimedes roadmap template, the Phases section serves this role. |

**Note:** These three overlap in practice — a small project's roadmap may contain its queue and plan in one doc (which is what Archimedes roadmaps do). The distinctions matter more as Kurt scales across many projects and needs to talk about these concepts separately. When Kurt says "here's the order I'd like in the queue," that's understood as updating the roadmap's What's Next section.

## Ideation & Capture Terms

| Term | Definition |
|---|---|
| **Brain dump** | Both verb and noun. As a verb: the act of dumping raw, unstructured thoughts — ideas, wishes, half-formed requirements — without worrying about format or organization. As a noun: the content produced by that act ("I've got a brain dump"). Brain dumps are the raw material that lives inside an idea bin. |
| **Idea bin** | The persistent container where brain dumps live. A `capture-` file in every project that's always open for new thoughts. Not just a kickoff tool — accumulates ideas across Chat sessions, Cowork sessions, and Kurt's own notes throughout a project's life. The idea bin feeds the Idea Bin pipeline. |
| **Idea Bin pipeline** | The end-to-end process for transforming raw ideas into structured project artifacts. Aliases: **brain dump pipeline**, **idea distillation pipeline**, **brain dump distillation pipeline**. Two entry paths: (1) brain dump path — messy thoughts in the idea bin, (2) prompt path — Kurt arrives with a semi-structured description. Both converge on two outputs: overview doc (for Kurt) and roadmap (for Claude). Reentrant — can run multiple times as new components emerge. The synthesis guide includes embedded overview creation guidance and roadmap creation guidance (absorbed from former ID9). |
| **Synthesis step** | The transformation at the core of the Idea Bin pipeline. Claude reads the bin (or semi-structured prompt) and produces two outputs: overview doc (Kurt's design surface) and roadmap (Claude's execution surface). Includes surfacing questions back to Kurt before generating. |

## Process Terms

| Term | Definition |
|---|---|
| **Sweep** | A systematic read-through of project folders to identify lessons, patterns, or issues. The project sweep reads all folders under Claude Cowork Folders/. |
| **Cleanup checklist** | A repeatable verification process that brings all project files into sync. Two modes: light (post-compaction, 2–3 min) and full (pre-push, 10–15 min). |
| **Audit** | A cold-session review of a project by a separate Claude task. The auditor has no prior context — reads what's on disk and gives suggestions. Catches builder blind spots. |
| **Compaction** | When Cowork summarizes earlier conversation to free up context. Information in conversation is lost; information in files survives. |
| **Cold start / Fresh session** | A new Claude session with zero prior context. The litmus test: can a cold session read the project folder and be productive immediately? |
| **50% cliff** | Working heuristic: treat ~50% context utilization as the quality ceiling. Degradation is gradual, not literal, but the model never self-reports quality loss. Past 50%, primacy/recency bias strengthens and middle-context content fades. |
| **3 strikes rule** | If the agent fails the same test 3 times, clear the session and reframe. The context is poisoned with failed approaches — more attempts make it worse, not better. |
| **Context poisoning** | When a session accumulates enough failed approaches, error messages, and abandoned strategies that the model's attention is split across more wrong paths than right ones. The 3 strikes rule is the fix. |
| **Work cycle** | The repeating pattern for non-trivial tasks: Explore → Plan → [Fresh] → Implement → Verify → Improve. Each phase ideally starts at full context capacity. The `[Fresh]` step is optional for small tasks but critical for anything that consumed significant context during planning. |
| **Harness** | The scaffolding that sets an agent up to succeed — CLAUDE.md, skills, MCP tools, templates, conventions. If the agent can't do something, that's a harness problem, not a model problem. |
| **Feedback loop** | The cycle: project does work → writes lessons-learned → Archimedes reads it → updates best practices → next project benefits. |
| **Harvest** | When Archimedes-builder reads lessons-learned files from multiple projects and pulls findings into the lessons learned library. |
| **Fresh-session standard** | The test for whether a project's files are complete: a cold-start Claude should be immediately productive. If Claude needs you to re-explain things that should be in files, something's missing. |
| **Autonomous build window** | The north star metric. How long Claude can operate without needing Kurt. Every Archimedes convention — pre-loaded keys, constraints files, proven patterns — extends this window. |
| **Design then Build** | A workflow mode (typically Opus). Kurt and Claude design together, then Claude goes autonomous for 15+ minutes while Kurt steps away. The autonomous build window is what makes this possible. |
| **Pair Build** | A workflow mode (typically Sonnet). Kurt and Claude work shoulder-to-shoulder in tight test-debug loops. Archimedes gives Sonnet a cold start with zero ramp-up. |

## Evaluation Framework Terms

| Term | Definition |
|---|---|
| **Touchstone** | The master evaluation framework. Three dimensions: Gates (priority stack), Phase (Build/Run), Who (Kurt/Claude/Systems). 3 × 2 × 3 = 18 cells. Every convention traces back to a gate. Owned by Archimedes. Source of truth: `for-claude/ref-5-kurt-design-principles-for-claude.md` (Principle #4). |
| **Gates** | The three evaluation criteria in strict priority order. Gate 1 must clear before Gate 2 matters. Gate 2 must reach threshold before Gate 3 is pursued. |
| **Gate 1: Safety & Security** | Binary gate (pass/fail). Two components: Security = unauthorized access or exposure. Safety = authorized agents making harmful mistakes. Nothing advances until it clears. |
| **Gate 2: Effectiveness** | Threshold gate. Does it work? Does it do the right thing? Must reach minimum viability before optimization begins. |
| **Gate 3: Efficiency** | Optimization gate. Continuous improvement. The reward for passing Gates 1 and 2. For Kurt, this means approving less and longer autonomous windows. |
| **Phase** | Build (creating and deploying) or Run (operating and maintaining). The Touchstone questions differ by phase. |
| **Who** | The three audience types: Kurt (judgment, oversight, design), Claude (constraints, scope, execution), Systems (compatibility, conventions, machine-readability). Different failure modes and mitigations per cell. |
| **Trust gradient** | The maturity model by which actions graduate from ACK → Soft NACK → Full NACK. Earned by demonstrating Gate 1 and Gate 2 compliance. Graduation can be revoked. |
| **Blast radius** | The scope of damage if an action goes wrong. Low blast radius → faster NACK graduation. High blast radius → slower graduation, possibly permanent ACK. |
| **Touchstone trace** | A brief statement at the top of a design doc identifying which gates that doc serves and why. Ensures any Claude session immediately knows the purpose behind the conventions. |
| **Traceability** | Every convention, SOP, or design decision should trace back to a specific gate. If it can't, it's dead weight or its justification is missing. |
| **Posture audit** | Research-based review of whether current standards reflect latest best practices. "What does the world know now that we didn't know last month?" |
| **Health audit** | Is the system working as designed? Services running, cron jobs firing, endpoints responding. Frequent (daily or continuous), automated, mechanical. Marvin owns. |
| **Security audit** | Is the system locked down? Repo visibility, env var exposure, access controls, API key rotation. Periodic (weekly/monthly + every deploy/install), checklist-based. Marvin runs, Archimedes owns the checklist. |
| **Three-Question Audit Frame** | Every audit validates the three-layer model: (1) Is the principle correct? (Layer 1), (2) Is the translation complete? (Layer 2), (3) Is the machinery working and output high quality? (Layer 2 → 3). |

## The Three-Layer Optimization Model

| Term | Definition |
|---|---|
| **Three-Layer Model** | The core architecture that makes Archimedes work. Three layers, each optimized for a different audience: Layer 1 (Kurt), Layer 2 (translation), Layer 3 (Claude). The acceleration framework: improving any one layer makes the whole system better. The key diagnostic skill is knowing which layer to improve. |
| **Layer 1 (optimized for Kurt)** | Clear, precise SOPs in plain language. One concept per SOP. Kurt states it once — that's it from his perspective. |
| **Layer 2 (the translation layer)** | The 1-to-many mapping between Layer 1 and Layer 3. One Kurt SOP may require writes into 8 different markdown files, each encoded per that file type's optimization contract. The SOP registry is the primary Layer 2 tool. |
| **Layer 3 (optimized for Claude)** | Best practices encoded in markdown so Claude sees the right thing, at the right time, without loading anything unnecessary. Structured for context windows, cold starts, and compaction survival. |
| **Rosetta Stone principle** | The 1-to-many translation from Layer 1 → Layer 3, governed by Layer 2. Named because it translates one language (Kurt's SOPs) into another (Claude's markdown). Design Principle #7. |
| **SOP registry** | The Layer 2 workhorse. Maps each plain-language SOP to every file where it must be reflected, with function tags (Remind, Teach, Catch, Inherit) per implementation point. When an SOP changes, the registry tells Claude exactly which files to update. Lives in `for-claude/ref-6-sop-registry-for-kurt-and-claude.md`. |
| **Two-Stack Model** | The three-layer model applied twice: Stack 1 (Builder — how Archimedes itself works, private repo) and Stack 2 (Product — what Archimedes ships to leaf projects, public repo). Each stack has its own Layer 1, Layer 2, and Layer 3. |
| **Preference stack** | The four surfaces that define how Claude behaves: web preferences, Cowork global instructions, personal CLAUDE.md, project CLAUDE.md. Archimedes owns all four. Seven sub-principles govern stack design, each tracing to a Touchstone gate. |
| **Harness** | The scaffolding that sets Claude up to succeed — CLAUDE.md, skills, MCP tools, templates, conventions. If Claude can't do something, that's a harness problem, not a model problem. |

## Architecture Terms

| Term | Definition |
|---|---|
| **Decision tree** | Archimedes's core routing principle. Not one-size-fits-all. Routes to the right patterns based on: what are you building? → what complexity? → what tools? → what templates? |
| **Build-decision-tree** | The decision tree that runs during project setup. Determines what modules, templates, and patterns to include. Lives in Archimedes, consumed during kickoff only — doesn't go into the project folder. |
| **Task-decision-tree** | The decision tree that runs within a project session. Task routing tables tell Claude which files to read for each task type. Lives inside the project folder. |
| **Conditional module** | A Archimedes module that's only loaded when a project uses a specific tool (Notion, Railway, Scrapfly, etc.). A leaf node on the build-decision-tree. |
| **Content mirror** | A local copy of external data (e.g., Notion database snapshot). Updated when the source changes. |
| **Structural map** | A local description of external structure (e.g., Notion page hierarchy). Updated when the structure changes, not when content changes. |
| **Subagent** | A separate Claude instance with its own clean context window. Heavy operations happen in the subagent's context, not the orchestrator's. Three patterns: Scout (explore and report), Adversarial Review (fresh-eyes check), Parallel Specialists (simultaneous domain work). |
| **Context containment** | The principle of keeping heavy operations (large file reads, MCP calls, codebase exploration) inside subagents so the orchestrator stays sharp. The orchestrator holds the map, not the territory. |

## Naming & Style Terms

| Term | Definition |
|---|---|
| **Audience tag** | The `for-[audience]` suffix on every file: `for-kurt`, `for-claude`, `for-kurt-and-claude`, `for-archimedes`. Determines writing style. |
| **`for-archimedes`** | Audience tag meaning: this file feeds back into Archimedes via the project registry. Written in `for-claude` style (technical audience, structured). Used for lessons-learned files. |
| **Sequence number** | The `##` in filenames. Controls read order within a folder. |
| **Last updated format** | `DDD DD MMM YYYY HHMM` — e.g., `Thu 12 Mar 2026 0007`. Military time. Used on all `for-kurt` files, READMEs, Notion pages, Google Sheets. |

## Kurt's Conceptual Shorthand

Kurt uses human-readable shorthand that maps to specific Archimedes files and conventions. When Kurt uses one of these terms, translate it to the right target — don't create a new file for the concept.

| Kurt says | He means | Where it lives |
|---|---|---|
| **"Touchstone"** | The master evaluation framework (3 gates × 2 phases × 3 whos). "Does this pass the Touchstone?" = evaluate through all three dimensions. "Which gate does this serve?" = trace a convention back to its root justification. | `for-claude/ref-5-kurt-design-principles-for-claude.md` (Principle #4) |
| **"ACK" / "NACK"** | Two action protocols governed by the Touchstone's trust gradient. **ACK-based:** "want me to do this?" — assumes inaction, waits for permission. **NACK-based:** "I'll do this unless you stop me" — assumes action, only stops on objection. Kurt's preference: always NACK. Actions graduate ACK → Soft NACK → Full NACK based on blast radius, reversibility, and track record. | `for-claude/ref-5-kurt-design-principles-for-claude.md` (Trust Gradient), `templates/router-readme-template.md` (Autonomy Rules) |
| **"SOPs"** (Standard Operating Procedures) | The conventions and procedures for a given domain (git, cleanup, naming, etc.). Not a standalone SOPs document. | Distributed across the relevant guide, reference, or template. "Update the GitHub SOPs" = update git/push conventions in `guides/session-discipline-guide.md`, naming conventions in `templates/naming-conventions.md` §5, etc. |
| **"Update the GitHub SOPs"** | Update git-related conventions (push process, branch naming, commit messages, etc.) | `guides/session-discipline-guide.md` (git workflow), `templates/naming-conventions.md` §5 (GitHub naming) |
| **"The naming doc"** | The naming conventions reference | `templates/naming-conventions.md` |
| **"The overview"** | The project overview doc | `{project}-overview-for-kurt.md` at project root |
| **"The roadmap"** | The project roadmap | `for-claude/design-1-roadmap-for-claude.md` |
| **"Layer 1 / Layer 2 / Layer 3"** | The Three-Layer Optimization Model: Layer 1 = optimized for Kurt (SOPs), Layer 2 = translation layer (1-to-many mapping), Layer 3 = optimized for Claude (markdown files). "Which layer broke?" is the diagnostic question. | See "The Three-Layer Optimization Model" section above. Source of truth: `ref-5` Architecture section. |

**General pattern:** Kurt thinks in concepts ("SOPs," "best practices," "the rules for X"). Archimedes stores those concepts in the file that's structurally right per our markdown conventions — usually a guide, reference, or the relevant section of an existing doc. When Kurt asks to update a concept, find where that concept lives and update it there. If the concept genuinely isn't captured anywhere, create it in the right file type per the file type taxonomy.

---

## GitHub & Workflow Terms

| Term | Definition |
|---|---|
| **Mac path** | The real filesystem path on Kurt's Mac. Recorded in every CLAUDE.md and registry entry because Cowork VM mount paths differ. |
| **Git workflow** | Cowork updates files → drafts copy-paste terminal commands for Kurt → commands always start with `cd` to the Mac path. |
| **`kurt316-ai`** | Kurt's personal GitHub account. Default for most projects including Archimedes. |
| **`kurt-ai-316`** | Kurt's Northslope GitHub account. Each project specifies which account it uses. |
| **Northslope** | Kurt's company. One word. Each project specifies which account it uses (personal: `kurt316-ai`, Northslope: `kurt-ai-316`). Archimedes is meta — used across both. |
