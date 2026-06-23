---
title: Audience Curator — Source List
version: 5
last_updated: 2026-06-23
description: RSS sources for the audience-curator agent. Substack-class only — Substack publications, authoritative independent blogs, NYT-class news. Hand-edited. Agent parses `## ` headers and `url:` lines; other fields are audit trail for Greg.
---

# Audience Curator — Source List

Substack-class sources for the audience scan. Hand-edit this file to add, remove, or annotate sources. The agent reads `## ` headers and `- url:` lines under each header; `author:`, `added:`, and `why:` are for Greg's audit trail and are ignored by the agent.

A future sibling agent (e.g., `listening-curator`) gets its own file in this folder (`listening.md`, etc.). Same format, different file. The convention scales.

## Simon Willison's Newsletter
- url: https://simonw.substack.com/feed
- author:
- added: 2026-05-14
- why:

## One Useful Thing
- url: https://www.oneusefulthing.org/feed
- author:
- added: 2026-05-14
- why:

## The Road to AI We Can Trust
- url: https://garymarcus.substack.com/feed
- author:
- added: 2026-05-14
- why:

## The Algorithmic Bridge
- url: https://www.thealgorithmicbridge.com/feed
- author:
- added: 2026-05-14
- why:

## Nate's Substack
- url: https://natesnewsletter.substack.com/feed
- author:
- added: 2026-05-14
- why:

## MKT1 Newsletter
- url: https://newsletter.mkt1.co/feed
- author:
- added: 2026-05-14
- why:

## The Product Compass with Paweł
- url: https://www.productcompass.pm/feed
- author:
- added: 2026-05-14
- why:

## Benedict Evans
- url: https://www.ben-evans.com/benedictevans?format=rss
- author: Benedict Evans
- added: 2026-05-14
- why: analytics-grounded tech commentary, weekly long-form, signal on shifting platforms (note — sporadic cadence; long gaps between posts expected)

## Platformer
- url: https://www.platformer.news/feed
- author: Casey Newton
- added: 2026-05-14
- why: tech-with-policy angle, honest critique, named-pattern commentary

## WSJ Tech
- url: https://feeds.content.dowjones.io/public/rss/RSSWSJD
- author: WSJ staff
- added: 2026-05-14
- why: financial/enterprise angle on AI; cultural context for business-leadership reading (the older feeds.a.dj.com URL is stale — using the current Dow Jones syndication endpoint). UNDER REVIEW as of 2026-06-23 (source-list v5) — sole surviving press feed; the rest of the establishment/news tier (NYT Tech, NYT AI, Wired AI, Stratechery, The Atlantic) was cut for ~0 keepers over 4 runs. Held to evaluate what it actually returns before deciding; Greg to look closely. All-time at cut: 5 keepers / 117 in-window.

<!-- Cut 2026-06-23 (source-list v5): the establishment/news tier — NYT Technology (0/107), NYT Artificial Intelligence (1/51), Wired AI (1/40), Stratechery (0/27), The Atlantic AI Watchdog (0/0, likely a broken feed). All were context-layer feeds, not keeper feeds, and the context value wasn't landing. Full history remains in feed-stats.md; re-adding later loses nothing. WSJ Tech held back deliberately for review (see its why note). -->

<!-- Added 2026-06-23 (source-list v4): marketing-ops practitioner sources to close the gap left by the generalist-AI-heavy original list. All feeds curl-verified live on 2026-06-23. On probation — kept or culled on feed-stats productivity, not reputation. Tier labels are from the distribution brief (agency-state-publishing/distribution/2026-06-23-linkedin-leverage-plan.md). -->

## The Marketing Operations Leader
- url: https://darrellalfonso.substack.com/feed
- author: Darrell Alfonso
- added: 2026-06-23
- why: Tier A — written for MOps leaders below the enterprise tier; shipping AI agents marketers actually use, MCP for marketers, "the job moves from running tools to designing the system that runs them." Healthy feed (~19 items)

## RevOps Impact
- url: https://revengine.substack.com/feed
- author: Jeff Ignacio
- added: 2026-06-23
- why: Tier A — concrete agent-orchestration and cost-per-workflow examples for revenue/marketing ops; real workflow building, mid-market altitude. Healthy feed (~19 items)

## Looped In
- url: https://demandloops.substack.com/feed
- author: Kaylee Edmondson (DemandLoops)
- added: 2026-06-23
- why: Tier A — demand-gen operator on AI-native plays, infrastructure debt, the identity crisis of teams adopting AI. Thin/sporadic feed (~3 items); judge on signal-per-post, not volume

## War on Mediocre Business
- url: https://scottmonday.substack.com/feed
- author: Scott Monday
- added: 2026-06-23
- why: Tier B — explicitly targets the $2M–$20M mid-market band; hands-on Claude Cowork series on turning AI from knowledge tool into execution agent. Very thin/new (~1 item); watch whether the back catalogue builds

## Vibe Working
- url: https://vibeproductmarketing.substack.com/feed
- author: Toni & Nik (fka Vibe Product Marketing)
- added: 2026-06-23
- why: Tier B — actionable AI for non-technical teams, no hype; Claude Cowork workflows for competitive intel and marketing tasks, anti-AI-slop method content. Healthy feed (~15 items)

## Almost Timely
- url: https://almosttimely.substack.com/feed
- author: Christopher Penn
- added: 2026-06-23
- why: Tier B — veteran marketer/data-scientist; applied generative-AI method for marketers. High publish volume — watch the keeper-rate-per-volume; cull if it behaves like the news feeds (NYT/WSJ pattern)

## Elena's Growth Scoop
- url: https://elenasletters.substack.com/feed
- author: Elena Verna
- added: 2026-06-23
- why: Tier C — strong AI-native angle (distribution when users are agents, retention when software is disposable). Borders on strategy think-piece; probation, keep only if it lands operational picks
