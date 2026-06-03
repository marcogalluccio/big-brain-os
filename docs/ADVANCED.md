# Advanced memory layer (optional)

Everything in this document is additive and opt-in. The Core memory system (frontmatter `name/type/status/last_touched`, the `MEMORY.md` index, four file categories, and soft-delete via `memory/archive/`) works perfectly without any of this. The Advanced layer extends individual files on a field-by-field, file-by-file basis. You can adopt one mechanic without the others, mix-and-match across files, and the default skills degrade gracefully when any of these fields are absent — they simply fall back to Core behavior.

---

## Salience score

Add `salience: <float>` to a file's frontmatter to express how front-of-mind that item should be right now, independent of its status emoji.

```yaml
---
name: website-redesign
type: project
status: 🟡
last_touched: 2026-06-01
salience: 0.85
---
```

**What it means:** a relevance weight from 0.0 to 1.0 representing how much cognitive attention this item deserves today. It is a subjective, time-varying number — update it during the session debrief when priority shifts.

**How `daily-briefing` uses it:** when `salience` is present, the skill sorts items by descending salience score before rendering the briefing. Items without a salience field are treated as neutral (equivalent to 0.5) and slotted after scored items of the same status tier.

**Choosing a value:**

| Range | Meaning |
|-------|---------|
| 0.8 – 1.0 | Front-of-mind — imminent deadline, active negotiation, needs action today |
| 0.5 – 0.7 | Default active work — progressing normally, check-in this week |
| 0.3 – 0.4 | Background — real but not pressing, revisit in 2+ weeks |
| < 0.3 | Dormant — still open, barely on radar |

**Absence:** if `salience` is not present, the skill treats it as neutral and falls back to status-based ordering. Nothing breaks.

---

## Takes (confidence fence)

Add a `## Takes` section inside any memory file to separate established facts from evolving opinions and hypotheses. This prevents the daily briefing and session debrief from treating uncertain beliefs as settled context.

Three confidence levels:

- 🟢 **High** — confirmed, verified, or witnessed directly
- 🟡 **Medium** — working hypothesis, likely true but not confirmed
- 🔴 **Low** — early signal, speculative, needs validation

**Worked example** (inside a `project_*.md` file, after the Status Log):

```markdown
## Takes

🟢 The client confirmed a May 31 deadline in writing.
🟢 Budget is capped at €8,000 — stated twice in calls.

🟡 They probably want a follow-on engagement after the workshop;
   the last call ended with "we'd love to do more of this."

🔴 The CTO might be the real decision-maker, not the CMO —
   noticed he asked most of the technical questions.
   Not confirmed, watch for it.
```

**Rules of thumb:**
- Keep the Takes section short — if it's growing large, the body context is doing the work instead.
- Promote a take from 🟡 → 🟢 the moment you confirm it; don't leave stale 🟡s around.
- The session debrief can update Takes inline when something gets confirmed or disproved.

---

## Soft-delete + recovery

The Core soft-delete rule is: set status ❌ and move the file to `memory/archive/`. The Advanced layer adds one field to make recovery and auditing easy:

```yaml
---
name: widget-partnership
type: project
status: ❌
last_touched: 2026-05-14
archived_at: 2026-05-14
---
```

**Why `archived_at`:** it records exactly when the item was closed, so you can audit the arc of a project (opened → touched → archived) and so any recovery is self-documenting.

**How to recover a file:**

1. Move it from `memory/archive/` back to `memory/`.
2. Change status from ❌ to the appropriate active emoji (🟡, 🟠, etc.).
3. Remove or blank out `archived_at`.
4. Restore the index line in `MEMORY.md` (move it out of the Archive section).

**Relation to Core soft-delete:** the Core defines *where* the file goes (the `archive/` folder). The Advanced layer just *dates* the move. Both mechanisms work together — you can archive without `archived_at` (pure Core) or archive with it (Core + Advanced). The recovery procedure is the same either way; `archived_at` just gives you the timestamp.

---

## Enabling all of it

There is nothing to install, configure, or enable globally. To use any part of the Advanced layer:

- **Salience:** add `salience: 0.5` (or your chosen value) to a file's frontmatter.
- **Takes:** add a `## Takes` section anywhere in the body of a memory file.
- **Archived-at:** add `archived_at: YYYY-MM-DD` to frontmatter when you close a file.

You can adopt one mechanic without the others, apply it to one file and not the rest, or never use any of it. The Core schema (`name`, `type`, `status`, `last_touched`) is always required; everything above is layered on top.
