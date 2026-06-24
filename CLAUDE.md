---
title: Claude Code guidance for agency-state-agents
description: Working instructions for Claude Code sessions operating in the Agency State agent-system repo
last_updated: 2026-06-23
---

This repo holds Agency State's **agents** — built and run here — plus the context they share. The audience-curator lives here; future agents get their own folder alongside it.

**This repo is PUBLIC.** Anything committed is publicly visible. No secrets, API keys, credentials, or private client data — ever. Private material belongs in the companion repos (`agency-state-publishing`, `agency-state-practice`) or outside version control.

## Layout

- `audience-curator/` — the RSS curation agent. `AGENT.md` is its role definition and run flow; `context/` holds its criteria, rules, and output format; `memory.md`, `curated-history.md`, `feed-stats.md` are its persistent state; `sources/` is its hand-edited feed list. It writes curation output to the **`agency-state-publishing`** repo's `curation/` folder.
- `_shared/` — context shared across agents: `brand-voice.md` (operational voice extract) and `about-greg.md` (founder + audience context). Shared so it isn't duplicated inside any one agent.
- `_shelved/` — parked agent designs not being built. Not active work.
- Each agent is one folder, marked by its own `AGENT.md`. Read that `AGENT.md` before operating or modifying the agent.

## Voice

Voice is **per-agent, not repo-wide** — each agent declares the voice it writes in, in its own `AGENT.md`. Don't assume the brand voice as a default.

- Brand voice (agents producing Agency State marketing/brand copy): pull via the brand MCP (`get_brand_voice`) or the `_shared/brand-voice.md` extract.
- Personal / Substack voice (agents whose output feeds Greg's Substack or personal channels): the reference lives with the agent or in `_shared/`, anchored to the example article — not the brand MCP.

## Conventions & git

- Frontmatter in markdown; lowercase-hyphen filenames; versions in files (archive filenames excepted).
- **Public repo** — focused, descriptive commits; never commit secrets or private content; no `.DS_Store`.
