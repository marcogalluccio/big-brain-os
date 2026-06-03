---
name: daily-briefing
description: Builds the day's work priorities by reading the memory index and the latest daily-log entry. Read-only — it never writes files. Use at the start of a working day or session. Triggers: "briefing", "daily briefing", "morning briefing", "what's on today", "build my briefing".
triggers:
  - "briefing"
  - "daily briefing"
  - "morning briefing"
  - "what's on today"
  - "build my briefing"
---

# Daily Briefing Skill

Reads the memory system and the most recent daily log, then builds a structured list of WORK priorities for the current day. Output is formatted as HTML and opened in the browser via `html-preview`.

This skill is **read-only**. It reads memory and logs; it never modifies any file.

## When to Use

Run this at the start of a working day or session.

Triggers: "briefing", "daily briefing", "morning briefing", "what's on today".

## Steps

1. **Read the memory index**
   Read `MEMORY.md`. Collect every active item (status 🔴🟠🟡🟢🔵) and its one-line hook. Open the underlying `memory/*.md` files only when you need a project's next action or deadline.

2. **Read the latest daily-log entry**
   Read the most recent file in `daily-log/` (today's if it exists, otherwise the most recent prior day). Look for:
   - tasks left pending or incomplete
   - notes and reminders carried forward
   - context on what was happening last session

3. **Order the priorities (graceful degradation)**
   This is the key sorting rule, and it adapts to whether the Advanced layer is in use:

   - **If memory items carry a `salience` field** (the optional Advanced field, 0.0–1.0; see `docs/ADVANCED.md`): sort by **descending salience first, then by status**. An item with no `salience` is treated as neutral (0.5) and slotted after scored items in the same status tier. This way a high-salience 🟡 can outrank a low-salience 🟡.
   - **If `salience` is not present** anywhere: fall back to **status alone** — order by 🔴, then 🟠, then 🟡, then 🟢, then 🔵.

   Either way, also surface anything from the latest daily log that was left incomplete. The skill must work whether or not `salience` is present; absence simply means status-only ordering. Never error out because Advanced fields are missing.

   If an item exposes a `## Takes` section, treat 🔴/🟡 takes as hypotheses, not settled facts — do not promote a speculative take into a hard priority.

4. **Build the briefing**
   Produce a markdown document with these sections:

   ```markdown
   # Daily Briefing — [Day, Date]

   ## Today
   - [ ] [Highest priority]
   - [ ] [Second priority]
   - [ ] [Third priority]

   ## Watch
   | Item | Status | Note |
   |------|--------|------|
   | [Stalled item] | 🟠 | [What you are waiting on] |

   ## Upcoming
   [Deadlines or events in the next 7 days]

   ## From the last log
   [Incomplete items or reminders carried forward]
   ```

5. **Render and open**
   Use the `html-preview` skill to render the briefing and open it in the browser.

## Rules

- **Read-only.** Never modify memory files, the index, or daily logs during this skill.
- If `MEMORY.md` does not exist, say so and suggest running setup.
- If there are no active items, produce a minimal briefing and note that memory is empty.
- Keep it concise — this is a scan, not a report.
