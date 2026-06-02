---
name: feed-stats
description: Append-only record of per-feed counts (items in window, items selected) per run. The curator reads this before writing the curation file and includes a rolling 4 / 8 / 12-run + all-time table in the output. Used to inform source pruning over time.
version: 1
---

# Feed Stats

Append-only. Each date section lists per-feed counts for that run.

Format per line: `feed_url | feed_name | in_window | selected`

Keyed on feed URL (stable across `## ` header renames in `sources/audience.md`). Display name is read from the current source list at run time, not from this file.

Pruning heuristic: roughly 12 consecutive runs (3 months at weekly cadence) of zero contribution = candidate for cull. Discretion overrides the heuristic — a sporadic publisher who lands a high-signal piece once a quarter still earns the slot.

## 2026-05-14
- https://simonw.substack.com/feed | Simon Willison's Newsletter | 1 | 1
- https://www.oneusefulthing.org/feed | One Useful Thing | 0 | 0
- https://garymarcus.substack.com/feed | The Road to AI We Can Trust | 3 | 2
- https://www.thealgorithmicbridge.com/feed | The Algorithmic Bridge | 3 | 1
- https://natesnewsletter.substack.com/feed | Nate's Substack | 8 | 3
- https://newsletter.mkt1.co/feed | MKT1 Newsletter | 0 | 0
- https://www.productcompass.pm/feed | The Product Compass with Paweł | 1 | 1

## 2026-05-22
- https://simonw.substack.com/feed | Simon Willison's Newsletter | 2 | 1
- https://www.oneusefulthing.org/feed | One Useful Thing | 0 | 0
- https://garymarcus.substack.com/feed | The Road to AI We Can Trust | 6 | 1
- https://www.thealgorithmicbridge.com/feed | The Algorithmic Bridge | 5 | 1
- https://natesnewsletter.substack.com/feed | Nate's Substack | 11 | 6
- https://newsletter.mkt1.co/feed | MKT1 Newsletter | 3 | 2
- https://www.productcompass.pm/feed | The Product Compass with Paweł | 2 | 1
- https://stratechery.com/feed/ | Stratechery | 8 | 0
- https://www.ben-evans.com/benedictevans?format=rss | Benedict Evans | 0 | 0
- https://www.platformer.news/feed | Platformer | 5 | 1
- https://www.nytimes.com/svc/collections/v1/publish/https://www.nytimes.com/spotlight/artificial-intelligence/rss.xml | NYT Artificial Intelligence | 11 | 0
- https://rss.nytimes.com/services/xml/rss/nyt/Technology.xml | NYT Technology | 31 | 0
- https://feeds.content.dowjones.io/public/rss/RSSWSJD | WSJ Tech | 32 | 2
- https://www.wired.com/feed/tag/ai/latest/rss | Wired AI | 10 | 0
- https://www.theatlantic.com/feed/category/ai-watchdog/ | The Atlantic — AI Watchdog | 0 | 0

## 2026-06-01
- https://simonw.substack.com/feed | Simon Willison's Newsletter | 2 | 1
- https://www.oneusefulthing.org/feed | One Useful Thing | 1 | 1
- https://garymarcus.substack.com/feed | The Road to AI We Can Trust | 5 | 0
- https://www.thealgorithmicbridge.com/feed | The Algorithmic Bridge | 3 | 2
- https://natesnewsletter.substack.com/feed | Nate's Substack | 9 | 5
- https://newsletter.mkt1.co/feed | MKT1 Newsletter | 3 | 1
- https://www.productcompass.pm/feed | The Product Compass with Paweł | 2 | 2
- https://stratechery.com/feed/ | Stratechery | 6 | 0
- https://www.ben-evans.com/benedictevans?format=rss | Benedict Evans | 1 | 0
- https://www.platformer.news/feed | Platformer | 3 | 1
- https://www.nytimes.com/svc/collections/v1/publish/https://www.nytimes.com/spotlight/artificial-intelligence/rss.xml | NYT Artificial Intelligence | 16 | 0
- https://rss.nytimes.com/services/xml/rss/nyt/Technology.xml | NYT Technology | 20 | 0
- https://feeds.content.dowjones.io/public/rss/RSSWSJD | WSJ Tech | 28 | 2
- https://www.wired.com/feed/tag/ai/latest/rss | Wired AI | 10 | 0
- https://www.theatlantic.com/feed/category/ai-watchdog/ | The Atlantic — AI Watchdog | 0 | 0
