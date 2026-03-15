# {PROJECT_NAME} — Glossary

**Last updated:** {DDD DD MMM YYYY HHMM PT}

Use these terms consistently across all project files. When in doubt, check here first. Prevents Claude from hallucinating meanings or using inconsistent terminology across sessions.

**Structure:** Archimedes Terms (universal, keep as-is) → Domain Terms → Project-Specific Terms → People & Accounts → Technical Terms.

**Rules:**
- Retired terms stay with a note: `Retired. Use {new term} instead.` Don't delete — future sessions might encounter the old term.
- Cross-project terms: add to lessons-learned under **Glossary term** category for Archimedes harvest.
- Update when: new term comes up that Claude might misinterpret, Kurt corrects a term, a term is retired or renamed.

<!-- ARCHIMEDES HEADER END — do not edit above this line -->

---

## Archimedes Terms (Universal — Include in Every Project)

| Term | Definition |
|---|---|
| **Archimedes** | The cross-project system of conventions, templates, guides, and infrastructure that governs how Kurt's projects are structured, documented, and maintained. The hub — all projects inherit from it. |
| **Archimedes protocols** | The full operating system Archimedes provides: folder structure (Two-Stack Model), file naming, cleanup checklist, mailbox communication, session discipline, writing style by audience, autonomy rules, and standing jobs. |
| **Two-Stack Model** | Folder architecture: Stack 1 (builder) = how the project works (`{project}-files-for-claude/`, `archimedes-mailbox/`, root files). Stack 2 (product) = what the project delivers (`output/`). Each stack has its own git repo. |
| **Archimedes mailbox** | Two-file communication channel (`archimedes-mailbox/inbox.md` + `outbox.md`) for bidirectional feedback between a project and Archimedes. Projects write to outbox; Archimedes writes to inbox. |
| **Standing jobs** | Eight outbound message types that run continuously: project-announce, new-pattern, anti-pattern, convention-update, convention-conflict, tool-insight, question, module-request. Write to `archimedes-mailbox/outbox.md` when spotted. |
| **NACK-based flow** | Default action model. "I'll do this unless you stop me" — assumes action, only stops on objection. |
| **`[KURT ACTION]`** | Tag for items requiring human judgment. Escalation marker that Kurt or the next session can scan for. |

## Domain Terms

| Term | Definition |
|---|---|
| *(Add project-specific domain terms here)* | |

## Project-Specific Terms

| Term | Definition |
|---|---|
| *(Add terms unique to this project here)* | |

## People & Accounts

| Name | Role / Context |
|---|---|
| Kurt (KFS) | Project owner. Personal account: kurt316-ai (GitHub), kurtoutdoors316@gmail.com. Work account: kurt-ai-316 (GitHub), kschwarz@northslopetech.com |

## Technical Terms

| Term | Definition |
|---|---|
| *(Add tech stack terms as decisions are made)* | |

---

## Maintenance Rules

**When to update this glossary:**
- A new term comes up in conversation that Claude might misinterpret later
- Kurt corrects Claude's use of a term
- A term is retired or renamed (mark it as retired, don't delete)

**Cross-project terms:** When a term from this project might be useful across other projects, add it to the lessons-learned file under the **Glossary term** category. Archimedes harvest will evaluate whether to promote it.
