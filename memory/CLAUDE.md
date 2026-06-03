# Memory operating rules

Read this before writing anything to memory.

## What memory is

`memory/` is the source of truth for active work: what is in progress, planned, decided, and learned. `MEMORY.md` is the index (one line per item). Each item is its own file holding the full context.

## Four categories

- `project_*` — active initiatives with a status and a next action.
- `strategic_*` — long-term positioning and directions.
- `feedback_*` — lessons learned and agent-behavior rules (include the why).
- `reference_*` — pointers to external resources (URLs, repos, dashboards).

## Index line format

`- [Title](file.md) - <emoji> <one-line hook>`

Status emoji: 🔴 urgent · 🟠 stalled/waiting · 🟡 active · 🟢 on track · 🔵 done but loose ends · ❌ closed.

## Frontmatter (Core)

```
---
name: <kebab-case-slug>
type: project | strategic | feedback | reference
status: 🟡
last_touched: YYYY-MM-DD
---
```

The Advanced layer adds optional fields (`salience`, `archived_at`) and a `## Takes` section. See `../docs/ADVANCED.md`. Skills must work whether or not those are present.

## Rules

- **Preserve-first.** Update the existing file rather than creating a duplicate. Check for an existing file before adding a new one.
- **Soft-delete.** Closing an item = set status ❌ and move its file to `memory/archive/`. Never hard-delete.
- **Don't save what the repo already records** (code structure, git history, what a CLAUDE.md already states) or what only matters to one chat.
- **Convert relative dates to absolute** before writing them.
- Link related items with `[[their-slug]]` in the body.
