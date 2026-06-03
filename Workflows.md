# Workflows

Cross-domain processes that span multiple folders or involve multiple steps.

<!-- CUSTOMIZE: This file documents recurring multi-step workflows.
     When a task involves more than one folder or more than one tool, it belongs here.
     Add your own workflows below. Remove the examples that don't apply to you. -->

Read this file when:
- Working on a task that touches multiple domains
- Running a recurring process end-to-end

---

## Workflow Template

Use this structure for each workflow:

**Trigger:** What starts this workflow (an event, a command, a recurring schedule)
**Steps:**
1. Step one
2. Step two
3. Step three
**Output:** What the workflow produces
**Files involved:** Which folders/files are touched

---

## Example Workflow 1: New client engagement

**Trigger:** A new client or project is confirmed

**Steps:**
1. Create a project file in `memory/` (`project_<name>.md`) with the starting context
2. Add an entry to `memory/MEMORY.md` with 🟡 status and the next action
3. Create a subfolder under `domains/clients-projects/` for the engagement's working files
4. Work across sessions, updating the project file through the session-debrief
5. When the engagement closes, set status to ❌ and archive the project file in `memory/archive/`

**Output:** A tracked engagement with full history
**Files involved:** `memory/`, `domains/clients-projects/`, `daily-log/`

---

## Example Workflow 2: Weekly work review

**Trigger:** Start of the week, or any time you want to reset priorities

**Steps:**
1. Read `memory/MEMORY.md` to see every active project and its status
2. Walk back through recent `daily-log/` entries to catch up on open threads
3. Re-prioritize: update statuses, next actions, and deadlines in the project files
4. Run the daily-briefing skill to produce the week's priority list
5. Close or archive anything that is done

**Output:** A clean, current view of what matters this week
**Files involved:** `memory/`, `daily-log/`

---

## Example Workflow 3: Learning to applied skill

**Trigger:** You start learning something new (a tool, a method, a topic)

**Steps:**
1. Capture the topic and your goal in `domains/learning-skills/Context.md`
2. Keep notes and references as you go in that domain folder
3. When the skill is good enough to use in real work, note it in the relevant project file
4. Log meaningful progress in the session-debrief so it is not lost between sessions

**Output:** A learned skill connected to where you actually apply it
**Files involved:** `domains/learning-skills/`, `memory/`, `daily-log/`
