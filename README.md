# Agency State Agents

This is the home for all Agency State agents. Each agent gets its own folder with its own `AGENT.md`, `memory.md`, `context/` folder, and `skills/` folder.

## Folder structure

```
agency-state-agents/
  README.md                        ← this file
  _shared/                         ← cross-agent context, used by every agent
    brand-voice.md                 ← canonical voice rules
    about-greg.md                  ← founder + business context
  [agent-name]/
    AGENT.md                       ← role, directives, instructions for the agent
    memory.md                      ← agent-specific learned preferences and corrections
    context/                       ← agent-specific reference files
    skills/                        ← reusable SOPs the agent can invoke
```

## Conventions

- **AGENT.md is the entry point.** Every agent starts by reading its own `AGENT.md`. The first directive in every `AGENT.md` is to read `memory.md` and update it in place when corrections happen.
- **Keep `AGENT.md` under ~200 lines.** When it grows past that, move detail into `context/` files and reference them from `AGENT.md`.
- **`_shared/` is read-only from the agent's perspective.** Agents reference it; they don't update it. Greg updates `_shared/` directly when brand or business context changes.
- **`memory.md` is the agent's mutable scratchpad.** Each agent has its own. Don't share memory across agents — voice drift and context contamination follow.
- **Skills are reusable, single-purpose SOPs.** When a process is solid enough to repeat, package it as a skill in `skills/` rather than embedding it in `AGENT.md`.

## Current agents

- **inoreader-curator** — Daily/on-demand RSS curation from Inoreader OPML exports. Outputs themed markdown files with draft react/share copy in Greg's voice.

## Adding a new agent

1. Create the folder: `[agent-name]/`
2. Create `AGENT.md` with the standard top directive (read memory, update in place) and a clear role definition
3. Create `memory.md` with empty section scaffolding
4. Create `context/` and add reference files as needed
5. Create `skills/` (empty initially)
6. If the agent needs cross-agent context (voice, business facts), reference `_shared/` from `AGENT.md`

## Personal vs. business

This folder is Agency State only. Personal and Early Returns agents live elsewhere. Don't mix.
