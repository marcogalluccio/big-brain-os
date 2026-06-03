---
name: memory-checkup
description: Read-only health audit of the memory system and the CLAUDE.md Structure claims. Cross-checks the MEMORY.md index against the files on disk, flags broken frontmatter and stale active projects, and checks each top-level CLAUDE.md "Structure" claim against reality. Produces a grouped report and proposes fixes — it never writes changes itself. Triggers: "memory checkup", "check my memory", "audit memory", "is my brain in sync", "memory health".
triggers:
  - "memory checkup"
  - "check my memory"
  - "audit memory"
  - "is my brain in sync"
  - "memory health"
---

# Memory Checkup Skill

A **read-only** audit of the memory system and the workspace's structural claims. It surfaces drift and incoherence, then **proposes** fixes. It **never writes or applies any change** — every fix is presented to the user for them to approve and run, or to hand to `session-debrief`.

## When to Use

Run on demand — periodically, or as a gate before shipping a batch of memory edits.

Triggers: "memory checkup", "check my memory", "audit memory", "is my brain in sync", "memory health".

## What it checks

Read `memory/CLAUDE.md` and `docs/ADVANCED.md` first so the audit follows the real rules.

### 1. Index ↔ files consistency
- For every **index line** in `MEMORY.md`, confirm a **matching file exists in `memory/`** (or in `memory/archive/` for items in the Archive section). Flag index lines pointing to a missing file (broken link).
- For every **`memory/*.md` file**, confirm it has an **index line** in `MEMORY.md`. Flag orphan files with no index line.
- **Exclude** the `*_template.md` files (`project_template.md`, `strategic_template.md`, `feedback_template.md`, `reference_template.md`) and everything under the `archive/` folder from the "must have an index line" requirement.

### 2. Core frontmatter integrity
For each non-template `memory/*.md` file, verify the Core frontmatter is present and well-formed: `name`, `type`, `status`, `last_touched`. Flag any file with missing, empty, or malformed Core fields. (The Advanced fields `salience`, `archived_at`, and the `## Takes` section are optional — never flag their absence.)

### 3. Stale active projects
Flag any item whose `last_touched` is **older than a threshold (default 30 days)** and is **still active** — i.e., status is **not** ❌ and **not** 🔵. These are candidates for a nudge, a status change, or archiving. Make the threshold easy to override if the user names a different one.

### 4. CLAUDE.md "Structure" ↔ disk
For each top-level `CLAUDE.md`, parse its **"Structure"** section and cross-check every declared folder/file against what is actually on disk:
- **Declared but missing:** a folder/file the Structure section claims, that does not exist on disk.
- **On disk but undeclared:** a top-level item that exists but is not mentioned in the Structure section.

## Report format

Produce one grouped report (render via `html-preview` if useful):

```
# Memory Checkup — [Date]

## 1. Index ↔ files
- Broken index links (file missing): ...
- Orphan files (no index line): ...

## 2. Frontmatter
- Files with broken/missing Core fields: ...

## 3. Stale active projects (> 30 days)
- [item] — last_touched YYYY-MM-DD, status 🟡

## 4. CLAUDE.md Structure drift
- Declared but missing on disk: ...
- On disk but undeclared: ...

## Proposed fixes (NOT applied)
- [grouped, concrete suggestions: add index line X, fix frontmatter Y, archive stale Z, update Structure for W]
```

## Rules

- **Read-only.** This skill never writes, edits, moves, or deletes any file. It only reads and reports.
- **Proposes, never applies.** Every fix is a suggestion for the user to approve. Applying them is a separate step (run it yourself, or via `session-debrief`).
- Exclude `*_template.md` files and the `archive/` folder from orphan-file checks.
- Degrade gracefully: never flag missing Advanced fields (`salience`, `archived_at`, `## Takes`) as errors.
- If `MEMORY.md` or `memory/` does not exist, report that and stop.
