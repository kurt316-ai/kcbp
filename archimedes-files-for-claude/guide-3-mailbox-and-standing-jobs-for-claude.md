# Mailbox Protocol & Standing Jobs

**Source:** Archimedes canonical push. Do not edit — updates come from Archimedes.
**Audience:** `for-claude` — cross-project communication protocol.

---

## Standing Jobs

These run continuously throughout every session — not just at cleanup. When you notice any of the following, write an entry to `archimedes-mailbox/outbox.md` immediately with status `unread`.

**The 8 outbound message types:**

1. **project-announce** — mandatory first entry during setup. Tells Archimedes this project exists.
2. **new-pattern** — something that worked well and should be added to Archimedes
3. **anti-pattern** — a failure mode that should be captured in the anti-patterns guide
4. **convention-update** — an Archimedes convention that doesn't work well; suggest a change
5. **convention-conflict** — an Archimedes convention that conflicts with what this project needs
6. **tool-insight** — something learned about a tool that other projects should know
7. **question** — "Should we be doing X?" when Archimedes doesn't have guidance
8. **module-request** — this project needs a module for something that doesn't exist yet

These map to the lessons-learned categories. If you'd capture it in lessons-learned, it probably also belongs in the outbox.

Don't batch these for cleanup. Write them when you spot them — conversation dies at compaction, outbox entries survive.

## Mailbox Structure

```
archimedes-mailbox/
├── inbox.md     ← FROM Archimedes (Archimedes writes, project reads)
└── outbox.md    ← TO Archimedes (project writes, Archimedes reads)
```

## Entry Format

```markdown
## Entry — DDD DD MMM YYYY HHMM PT
**Status:** unread | harvested | actioned
**Type:** {one of the 8 message types}
**Topic:** [short description]
**Content:**
[structured content]
```

## Ordering & Scanning

**Newest first.** New entries go at the top of the file (immediately after the header block and `---` separator). This applies to both inbox and outbox.

**Stop marker.** Every mailbox file contains an HTML comment that marks the boundary between unprocessed and processed entries:

```markdown
<!-- ACTIONED BELOW — stop scanning -->
```

When scanning a mailbox, read from the top and **stop at this marker.** Everything below it has already been handled. When you action the last `unread` entry, move the marker above it.

*Why:* Newest-first plus a stop marker means sessions never read stale history. The actionable surface is always between the header and the marker — which could be zero entries (nothing to do) or a handful (all recent).

## When to Write

- **Outbox:** Write immediately when you spot something (see Standing Jobs). The Project Health Checklist Section 9 is the backstop. Insert new entries at the top (above the stop marker).
- **Inbox:** Check for `unread` entries above the stop marker at session start (see session open protocol). Mark entries `actioned` after processing, then move the stop marker above the newly actioned entries.
