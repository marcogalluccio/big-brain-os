# Setup Guide

This is the technical setup for Big Brain: clone the repo, install the Superpowers plugin, and put memory where Claude Code can auto-load it. The hands-on, content-first walkthrough lives in [WELCOME.md](WELCOME.md); this file is the plumbing.

---

## Step 1: Clone the repo

```bash
git clone https://github.com/marcogalluccio/big-brain.git my-brain
cd my-brain
```

Rename the folder to whatever makes sense for you (e.g., `brain`, `work`, `my-brain`). Open it in Claude Code.

---

## Step 2: Install the Superpowers plugin

Superpowers is the base way of working in this brain. Install it before you do anything else.

In Claude Code, run:

```
/plugin
```

Then install **Superpowers**. The setup walkthrough in WELCOME.md runs through its `brainstorming` skill, so this needs to be in place first. The other recommended plugins are listed in [docs/TOOLBELT.md](docs/TOOLBELT.md); install them when a task calls for them.

---

## Step 3: Fill in your context

Two files hold your context:

- `About Me - Context.md`: who you are, your role, how you like to work.
- `Work - Context.md`: what your work is about, who it is for, what you are building.

You can edit them directly, but the recommended path is to let the agent guide you through it with the Superpowers `brainstorming` skill (see WELCOME.md, Step 1). One question at a time beats a blank file.

---

## Step 4: Set up your domains

Each area of your work gets a folder under `domains/`. The repo ships with a few example domains. Adapt them, or add your own:

```bash
cp -r domains/content domains/marketing
```

Then edit the `CLAUDE.md` and `Context.md` inside each domain folder. Delete any example domains you do not need.

---

## Step 5: Set up the memory system

The `memory/` folder in this repo contains templates. In real use, memory lives where Claude Code auto-loads it:

```
~/.claude/projects/[your-workspace-path]/memory/
```

Claude Code reads `MEMORY.md` from this path when you open your workspace. The path is your workspace's absolute path with slashes turned into dashes.

To set it up:

```bash
# Replace [your-workspace-path] with your actual path (dashes replace slashes).
# Example: ~/Desktop/my-brain  ->  -Users-yourname-Desktop-my-brain
MEMORY_PATH="$HOME/.claude/projects/-Users-$(whoami)-Desktop-my-brain/memory"
mkdir -p "$MEMORY_PATH"
cp memory/*.md "$MEMORY_PATH/"
```

Then open `MEMORY.md` in that folder and clear out the example entries. Keep the headers, start fresh.

---

## Step 6: Run your first session

Open your workspace in Claude Code and type:

```
briefing
```

The agent reads `MEMORY.md` and any recent daily logs, then gives you a priority list. On first run it will be mostly empty. Add your first project to `memory/MEMORY.md` and run it again.

At the end of a session, type:

```
debrief
```

The agent asks what you worked on and what is blocked, logs the session to `daily-log/`, and updates your project files in memory.

---

## Optional: the advanced memory layer

Once the core loop feels natural, [docs/ADVANCED.md](docs/ADVANCED.md) describes an optional, opt-in layer on top of memory (salience scoring and more). Everything there is additive: the core system works fully without it.

---

## That's it

The system is running. From here:

- Add projects to `memory/MEMORY.md` as they come up.
- Use `briefing` to start, `debrief` to close.
- Use `preview` to render any document in the browser.
- Reach into [docs/TOOLBELT.md](docs/TOOLBELT.md) when a task needs a sharper tool.
