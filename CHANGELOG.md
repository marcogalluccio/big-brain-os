# Changelog

## 1.1 - 2026-06-11
- Self-improving skills: every native skill carries a `## Self-improvement` footer that logs friction to `skills/_improvements/friction-log.md` (protocol in `capture.md`); new `skill-improve` meta-skill turns logged friction into approvable diffs.
- Computed salience: optional deterministic formula (recency + deadline proximity + status weight + pinned − decay) documented in `docs/ADVANCED.md`, with the `pinned` and `evergreen` fields.
- Daily-log conventions: new `daily-log/CLAUDE.md` with deterministic `### Remember YYYY-MM-DD` reminders; `daily-briefing` resurfaces them on the target day, `session-debrief` files them.

## 1.0 - 2026-06-03
- First public release of Big Brain OS: a personal operating system for your work, built for Claude Code. Evolution of the original Big Brain workspace template.
- Two-level memory: light Core + opt-in Advanced layer (salience, takes, soft-delete).
- Four native skills: daily-briefing, session-debrief, memory-checkup, html-preview.
- Superpowers-first onboarding; recommended toolbelt (Superpowers, impeccable, deep-research).
- domains/ container with three example work domains.
- MIT license, CONTRIBUTING, examples marked deletable.
