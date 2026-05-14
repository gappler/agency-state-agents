---
title: Inoreader Curator — How to Run
version: 0.1.0
last_updated: 2026-05-09
---

# Inoreader Curator — How to Run

The agent's behavior lives in `AGENT.md`. This file is just the launch instructions.

## Normal run (interactive)

```
cd inoreader-curator
claude
```

(Run from the `agency-state-agents` repo root.)

Then in the session:

> Read AGENT.md and run as the inoreader-curator agent.

The first directive in `AGENT.md` points the session at `memory.md`, then the run flow in `AGENT.md` takes over. You can stop after each step or let it run end to end.

## Headless (one-shot)

For unattended runs — e.g., the eventual launchd path:

```
claude -p 'Read AGENT.md in the current working directory and run the inoreader-curator end to end.'
```

— invoked from this folder.

Two caveats before you wire this up:

- **Headless stalls on tool-approval prompts.** A real unattended run needs `--dangerously-skip-permissions` or a pre-approved tool allowlist configured in settings. Don't add the flag casually.
- **`context/operational-rules.md` still scopes out scheduled/autonomous runs.** Lift that before adding launchd.

## v0.1 caps still in effect

Per `context/operational-rules.md`: first 10 feeds, 1-day window, 100 candidate cap. The OPML now has 8 feeds total, so the feed cap is moot; the time and candidate caps still apply.
