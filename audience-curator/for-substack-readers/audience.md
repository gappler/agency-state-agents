---
title: Audience Curator — Source List
version: 3
last_updated: 2026-05-15
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

## Stratechery
- url: https://stratechery.com/feed/
- author: Ben Thompson
- added: 2026-05-14
- why: strategic tech/business analysis, named frameworks (aggregation theory etc.), practitioner-credible, honest reads on what tech delivers

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

## NYT Artificial Intelligence
- url: https://www.nytimes.com/svc/collections/v1/publish/https://www.nytimes.com/spotlight/artificial-intelligence/rss.xml
- author: NYT staff
- added: 2026-05-14
- why: cultural context the buyer's leadership reads; AI conversation at establishment tier. Uses the NYT spotlight collection-publish endpoint — an internal service URL, not advertised on NYT's public RSS index, but returns valid RSS for the AI spotlight page

## NYT Technology
- url: https://rss.nytimes.com/services/xml/rss/nyt/Technology.xml
- author: NYT staff
- added: 2026-05-14
- why: documented public NYT feed; kept as a stable fallback alongside the AI spotlight feed in case the internal /svc/collections/ endpoint changes or disappears

## WSJ Tech
- url: https://feeds.content.dowjones.io/public/rss/RSSWSJD
- author: WSJ staff
- added: 2026-05-14
- why: financial/enterprise angle on AI; cultural context for business-leadership reading (the older feeds.a.dj.com URL is stale — using the current Dow Jones syndication endpoint)

## Wired AI
- url: https://www.wired.com/feed/tag/ai/latest/rss
- author: Wired staff
- added: 2026-05-14
- why: occasional strong long-form on AI, scope-limited to AI tag to avoid consumer/gadget noise

## The Atlantic — AI Watchdog
- url: https://www.theatlantic.com/feed/category/ai-watchdog/
- author: Atlantic staff
- added: 2026-05-15
- why: long-form AI reporting at establishment tier; AI-specific category feed (Atom, not RSS, but standard feed format)
