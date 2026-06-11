---
name: session-debrief
description: End-of-session review. Writes a session summary into today's daily log and updates the relevant memory files (and their MEMORY.md index lines) when a status changes. Writes only to memory and daily-log. Triggers: "debrief", "wrap up", "close session", "log session", "what do we save".
triggers:
  - "debrief"
  - "wrap up"
  - "close session"
  - "log session"
  - "what do we save"
---

# Session Debrief Skill

Captures what happened in the current working session, updates the memory system when status changes, and appends a summary to today's daily log.

**Scope:** this skill writes **only** to `memory/` and `daily-log/`. It never touches code, domain folders, or anything else.

## When to Use

Run this at the end of a working session, before closing Claude Code.

Triggers: "debrief", "wrap up", "close session", "log session".

## Steps

1. **Ask the user three questions** (one at a time, waiting for each answer)
   - "What did you work on in this session?"
   - "What got completed or moved forward?"
   - "What is blocked, pending, or needs follow-up?"

2. **Identify which memory items were touched**
   From the answers, determine which `memory/*.md` files need updating. Read those files before changing them. Read the relevant rules in `memory/CLAUDE.md` first.

3. **Update memory files (preserve-first)**
   **Preserve-first**: always update the existing file rather than creating a duplicate. Check for an existing file before adding a new one. For each touched item:
   - update `next_action` if it changed
   - update the `status` emoji if the item moved forward or stalled
   - bump `last_touched` to today's date (verify the date first)
   - append a dated line to the `## Status Log` section
   - if the file uses the Advanced layer, update `salience` when priority shifted and refine any `## Takes` entries that got confirmed or disproved. If those fields are absent, skip them — never add them just to add them.

4. **Closing an item (soft-delete to archive)**
   When an item is done and closed:
   - set its `status` to ❌
   - **move the file into `memory/archive/`** (soft-delete; never hard-delete)
   - if the user uses the Advanced layer, also set `archived_at: YYYY-MM-DD` in frontmatter
   - move its index line in `MEMORY.md` down to the Archive section

5. **Update the MEMORY.md index**
   Reflect every status change in the one-line index entries. Only edit lines for items whose status or hook actually changed — leave the rest untouched.

6. **Write today's daily-log entry**
   Append a session summary to `daily-log/YYYY-MM-DD.md` (verify the date first). Create the file if it does not exist. Never overwrite or delete existing entries — only append.

   If something must happen on a specific **future** day, file it under a `### Remember YYYY-MM-DD` sub-heading (ISO date of the target day) in **today's** log — the `daily-briefing` skill resurfaces it on the target day. Do not bury forward-dated items inside generic Pending lines. Conventions in `daily-log/CLAUDE.md`.

   ```markdown
   ## Session — [HH:MM]

   **Worked on:** [what was done]

   **Completed:** [what moved forward or closed]

   **Pending / Follow-up:**
   - [item 1]
   - [item 2]
   ```

7. **Confirm**
   Tell the user which memory files were updated, which (if any) were archived, and the path of the daily-log entry written.

## Rules

- Always ask the three questions before writing anything.
- Do not invent what was worked on — use only what the user says.
- **Preserve-first:** update existing files; never duplicate. If a mentioned item has no file, offer to create one.
- **Soft-delete only:** closing = status ❌ + move to `memory/archive/`. Never hard-delete a memory file.
- Convert relative dates to absolute before writing them.
- Keep log entries factual and brief — a record, not a narrative.

## Self-improvement

At the end of the run, check it against these friction triggers (keywords): **avoidable round-trip · improvisation · breakage · token waste · user correction** (full definitions in `skills/_improvements/capture.md`). If at least one fired, ask the user *"there was friction on X — should I log it?"*; on ok, append a 3-line entry to `skills/_improvements/friction-log.md` per `capture.md`. Clean run → say nothing. Never self-edit this skill; improvements go through `skill-improve`.
