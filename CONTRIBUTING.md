# Contributing

Big Brain is a template. Most people fork it and make it their own, and that is the point. Contributions back to the template are welcome when they make the base system clearer, safer, or more useful for everyone.

## Proposing a skill

A skill is a folder under `skills/` with a single `SKILL.md`. To propose one:

1. Keep it self-contained: everything the skill needs lives in its folder.
2. Start `SKILL.md` with frontmatter (`name`, `description`, trigger phrases) so Claude Code can discover it.
3. Make it generic. A contributed skill should help any user, not encode one person's private workflow. Personal skills belong in your fork, not the template.
4. Open a pull request describing what the skill does and when it triggers.

## Proposing a domain

Domains live under `domains/`, one folder per area of work, each with a `CLAUDE.md` and a `Context.md`. The three that ship (`clients-projects/`, `learning-skills/`, `content/`) are examples. If you think a different example domain would help newcomers more, propose it the same way: a `CLAUDE.md` that explains the area and a `Context.md` template with clearly marked placeholders.

## Style conventions

- File and frontmatter conventions for memory follow `memory/CLAUDE.md`. Read it before touching anything under `memory/`.
- Structure (headers, labels, frontmatter keys) stays in English. Content can be in whatever language fits.
- In public-facing prose (README, CONTRIBUTING), avoid em-dashes and double-hyphens. Use commas, colons, periods, or parentheses.
- Mark example files as deletable so users know they can remove them.

## What not to commit

- Secrets: API keys, tokens, passwords, `.env` files.
- Personal data: real client names, contacts, private project details, anything you would not publish.
- Large binaries: images, video, archives. Reference heavy assets externally instead.
- Generated or local-only output: build artifacts, editor configs, OS junk.

When in doubt, leave it out. The template should stay clean enough that a stranger can clone it and understand it in minutes.
