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
