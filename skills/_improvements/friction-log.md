# Friction log

Append-only telemetry of skill friction. Written by each skill's
`## Self-improvement` footer (protocol in `capture.md`), consumed by the
`skill-improve` skill. Doubles as a dashboard: the skill with the most open
entries is the best improvement target.

Entry format (see `capture.md`):

```
## YYYY-MM-DD · <skill-name> · <friction|breakage>
what: ...
cost: ...
```

New entries go directly below this line, newest first. When `skill-improve` turns
entries into an accepted change, it moves them down to the Archive section.

---

## Archive

(Consumed entries land here, with a note on what changed.)
