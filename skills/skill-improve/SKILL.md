---
name: skill-improve
description: Analyzes an existing skill and its recorded friction in the friction log, then proposes concrete diffs to make it more effective and efficient (fewer round-trips, fewer tokens, clearer steps). Read-and-propose only — it never modifies a skill without explicit approval, diff by diff. Triggers: "skill-improve", "improve the X skill", "optimize the X skill", "evolve the X skill", "review the X skill".
triggers:
  - "skill-improve"
  - "improve the skill"
  - "optimize the skill"
  - "evolve the skill"
  - "review the skill"
---

# Skill Improve

Meta-skill: turns a skill's recorded friction into an approvable improvement
proposal. Never self-applying: propose a diff, the user decides, diff by diff.

This is the second half of the self-improvement loop. The first half is the
`## Self-improvement` footer each skill carries: it logs friction into
`skills/_improvements/friction-log.md` during normal use (protocol in
`skills/_improvements/capture.md`). This skill consumes that log.

## Input

`skill-improve <skill-name>` — e.g. `skill-improve session-debrief`.
If the name is omitted, show the ranking of skills by number of open entries in
the friction log and ask which one to take.

## Workflow

### 1. Gather context
- Find and read the target skill's `SKILL.md` (`skills/<name>/SKILL.md`),
  including any support files it cites, if relevant to the friction.
- Read `skills/_improvements/friction-log.md` and filter the **open** entries for
  that skill (ignore the `## Archive` section).

### 2. Diagnose
- Group the entries by pattern (same step, same recurring trigger).
- A recurring pattern is worth more than a one-off isolated friction: say so
  explicitly and prioritize patterns.
- If there are no open entries for that skill: say so and stop. No proposal
  without data (offer at most a light qualitative review, but only if the user
  explicitly asks for it).

### 3. Propose (on screen, do not write yet)
For each pattern present:
- **Symptom** — what happens and how often (cite the entry dates).
- **Cause** — which part of the SKILL.md provokes it.
- **Proposed diff** — the exact change to the SKILL.md (before → after), oriented
  to effectiveness + efficiency.
- **Cost/risk** — what could break. Conservative default: additive before rewrite.

Present all the proposals, then stop and wait for the user's ok, diff by diff.

### 4. Apply (only the diffs the user approves)
- For each accepted proposal, edit the `SKILL.md` with a targeted edit (not a
  full-file rewrite).
- Move the consumed entries from the open section to the `## Archive` section of
  the friction log, noting the date and what changed.
- Changes enter your normal git flow. Never push without permission.

## Rules

- **Never apply without explicit approval**, assessed diff by diff.
- **Additive first**: do not touch the skill's working logic unless it is the
  recorded cause of the friction. The goal is to refine, not rewrite.
- **No proposals without data**: empty log for that skill → no diff.
- **One skill at a time.**
- Never modify a skill's `## Self-improvement` footer (it is standard and
  uniform): if it needs changing, that is a change to `capture.md`, not to the
  single SKILL.
