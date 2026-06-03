# Welcome to Big Brain

You just cloned this repo. Good. Here is what you have and what to do next.

---

## What is this?

Big Brain is a personal operating system for your work, built for [Claude Code](https://claude.ai/code). Instead of explaining yourself every time you open a chat, you build a structured workspace that the agent reads automatically. Every conversation starts with your context already loaded: who you are, what you work on, and what you are doing right now.

The brain is the context and the memory. The method (how you plan, build, debug, research) comes from a small curated toolbelt of plugins, starting with Superpowers. You will install that first.

---

## How it works (short version)

Three ideas make this work:

**1. CLAUDE.md hierarchy: layered context**
Every folder has a `CLAUDE.md` that tells the agent what that area is about. The root one loads on every conversation. Subfolder ones load when you work in that area. You never re-explain yourself.

**2. File-based memory: continuity across sessions**
Projects, decisions, and lessons learned live in a `memory/` folder. The agent reads it when you start and updates it when you finish. Nothing gets lost between conversations.

**3. Work-domain subfolders: organized work**
Each area of your work (clients, content, learning, whatever fits) gets its own folder under `domains/` with its own context. The agent only reads what is relevant to the task.

---

## Your first run

Three steps. Do them in order.

### Step 0: Install Superpowers first

Before you touch anything else, install the Superpowers plugin. It is the base way of working in this brain: brainstorming, planning, test-driven development, and debugging all run through it.

In Claude Code, run:

```
/plugin
```

Then install **Superpowers**. That is it. You now have the discipline layer that the rest of the setup relies on.

### Step 1: Set up the brain as a brainstorm

Do not fill the context files in alone. Let the agent walk you through it.

Open this folder in Claude Code and say:

```
Let's set up my Big Brain. Use the Superpowers brainstorming skill.
```

The agent will invoke the Superpowers `brainstorming` skill and guide you one question at a time to fill in:

- `About Me - Context.md`: your name, your role, what you actually do day to day, how you like to work.
- `Work - Context.md`: what your work is about, who it is for, what you are building.
- Your first domains under `domains/`: pick the one or two areas of work you want to manage here, and shape their context.

Answering one question at a time is the point. You learn the Superpowers way of working while you build your brain, and the agent ends up with real context instead of placeholders.

### Step 2: Meet your toolbelt

Superpowers is the core, but it is not the only tool worth having. Open:

```
docs/TOOLBELT.md
```

It lists the recommended plugins and skills for work (building polished interfaces, deep verified research) with a one-line note on when to reach for each, plus the `html-preview` skill that already ships native in this brain. Install the rest when a real task calls for them, not before.

---

## When you are stuck

- **The agent does not know your context:** check that `About Me - Context.md` and `Work - Context.md` are filled in, not still placeholders.
- **Superpowers commands do nothing:** confirm the plugin installed cleanly via `/plugin`.
- **You want a new area of work:** add a folder under `domains/` and fill in its `CLAUDE.md` and `Context.md`.

---

## When you are ready for more

Read [SETUP.md](SETUP.md) for the technical setup (clone, memory path, plugins).

Read [docs/ADVANCED.md](docs/ADVANCED.md) when you want the optional advanced memory layer.

Read the [README](README.md) for the full picture of how the system is designed.

Good luck.
