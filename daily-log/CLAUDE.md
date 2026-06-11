# daily-log/

Per-day session record. One file per calendar day.

## Convention

- Filename: `YYYY-MM-DD.md`. ISO date. Verify the day of the week before writing
  it anywhere (see the date-verification rule in the root `CLAUDE.md`).
- Top of the file: a `# YYYY-MM-DD` heading, nothing else.
- Session entries use level-2 headings: `## Session — HH:MM` (24-hour clock),
  written by `session-debrief`.

## Filing reminders

- "note for today" → a `### Notes` sub-heading. Not a scheduled task.
- "remind me tomorrow" → a `### Remember YYYY-MM-DD` sub-heading with tomorrow's
  ISO date.
- "remind me on <day>" / "remind me on the <date>" → `### Remember YYYY-MM-DD`
  with the ISO date of the target day. Written in the log of the day you say it,
  not in a future log. The `daily-briefing` skill resurfaces this section on the
  target day and promotes it to Today.

## Anti-patterns

- Do not bury forward-dated pending items inside generic entries (e.g.
  `Pending: ... (next Monday)`). If something must happen on a specific future
  day, file it under `### Remember YYYY-MM-DD`. Generic Pending lines with
  parenthetical dates are not deterministically resurfaced by the briefing.
- Do not use the daily log as a project tracker: status, next actions, and
  deadlines live in `memory/`. The log records what happened.
