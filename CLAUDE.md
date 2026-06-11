# [YOUR WORKSPACE NAME]

<!-- CUSTOMIZE: Replace the title above with your workspace name, and the line below
     with a 2-3 sentence description. This is your personal operating system for WORK:
     a single brain where your professional context and memory live, so Claude Code
     understands who you are and what you are working on before doing anything.
     Example: "Personal work brain for Jane Doe — freelance product designer in Berlin.
     Covers client projects, content, and ongoing skill development." -->

[Short description of this personal work brain and what it covers.]

## Context files

- `About Me - Context.md` — who you are professionally: role, working style, expertise, goals.
- `Work - Context.md` — your work context: company, freelance practice, or studio. Optional; fill in if relevant.

## Agent Boot Sequence

### First Run Check

On every new conversation, silently check whether the workspace has been set up:
- Read `About Me - Context.md`. If it still contains the placeholder string `[Your full name]`,
  treat this as a first-time user.

**If first run:** read `WELCOME.md` and deliver its onboarding — install the Superpowers
plugin, then run guided setup via the `brainstorming` skill. Walk one step at a time, waiting
for confirmation before moving on. Do not proceed with any other work until setup is complete.

**If already configured:** skip `WELCOME.md` entirely and proceed with the Normal Boot below.

### Normal Boot

Auto-loaded by Claude Code (no action needed):
- This file (`CLAUDE.md`)
- The memory index `MEMORY.md`

On every conversation, before starting any task:
1. Read today's daily log: `daily-log/YYYY-MM-DD.md` (if it exists).
2. Read the `CLAUDE.md` of whatever domain the task touches.

Load on demand (only when the task requires it):
- `About Me - Context.md` — for tasks involving your voice, style, or positioning.
- `Work - Context.md` — for formal documents, outreach, anything organization-facing.
- `Workflows.md` — for multi-domain processes and pipelines.
- Domain `Context.md` files — when working deep inside a specific domain.

### Skills

Skills live in `skills/`, one folder per skill with a `SKILL.md` (instructions plus trigger
phrases). Setup wires them into Claude Code's discovery path via a `.claude/skills` symlink
(see `SETUP.md`, Step 5). Fallback: if the user says a skill trigger (like "briefing",
"debrief", "preview") and the skill has not loaded automatically, read the matching
`skills/<name>/SKILL.md` and follow it.

## Structure

- `About Me - Context.md` — personal professional profile: role, style, expertise, goals.
- `Work - Context.md` — your company, freelance practice, or studio context (optional).
- `domains/` — one subfolder per area of your work, each with its own `CLAUDE.md` and `Context.md`.
- `memory/` — file-based memory: active projects, strategy, feedback, references.
- `daily-log/` — session record, one file per day.
- `skills/` — your automation skills (briefing, debrief, preview, and any you add).
- `docs/` — engineering docs for the brain itself, including the optional Advanced memory layer.
- `Workflows.md` — cross-domain processes and pipelines.

## Memory System

Memory lives in `memory/`, indexed by `MEMORY.md` (one line per item, with status). Four categories:
- **Project** — active work with status, next action, and deadline. Updated by debrief.
- **Strategic** — long-term positioning and directions. Updated when strategy shifts.
- **Feedback** — lessons learned and agent behavior rules. Updated when you correct the agent.
- **Reference** — pointers to external resources (URLs, repos, deployments).

`MEMORY.md` is the dashboard; individual files hold full context. Closed items are soft-deleted
to `memory/archive/` (kept for historical recall, loaded on demand). The operating rules of the
layer (index format, preserve-first, anti-patterns) live in `memory/CLAUDE.md` — read it before
writing to memory.

An optional **Advanced layer** (salience, takes, soft-delete refinements) is documented in
`docs/ADVANCED.md`. Opt in only if you want it; the Core layer above works on its own.

## Rules

- **Never change any CLAUDE.md without asking the user first.** Why: these files affect how every
  agent in the system behaves.
- **Co-create on structural changes** (CLAUDE.md, memory, skills): propose options and get
  confirmation, never rewrite solo. Why: structure changes ripple across every future session.
- **ASCII-wireframe before building any visual UI** (dashboard, landing page, deck, email template),
  and get approval first. Why: cheaper to redirect a sketch than to rebuild code.
- **Date-verification rule:** before writing any date anywhere, verify the day of the week with
  `date -j -f "%Y-%m-%d" "YYYY-MM-DD" "+%A %Y-%m-%d"`. Why: computing day-of-week mentally is a
  recurring, universal bug — keep this rule.
- **Em-dash / double-hyphen avoidance in external-facing copy** (posts, emails, public pages,
  client deliverables): use commas, colons, semicolons, periods, or parentheses instead. Internal
  files and chat are exempt. Why: a house-style preference. _Optional: remove this rule if you do
  not care._
- **Language:** English for structure (headings, frontmatter, recurring labels like Status /
  Next action / Why). Your own language for content (notes, drafts). Outputs follow the recipient's
  language, not the source. Why: keeps the scaffolding consistent while content stays natural.
