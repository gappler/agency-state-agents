# Operational Rules

Guardrails, scope boundaries, and run configuration. These rules are stable — they don't change run-to-run. If they need to change, update this file rather than overriding it in conversation.

## Run configuration

- **Window: 10 days.** Filter candidate items to the trailing 10 days from the run date. Targets a weekly Friday run rhythm; the 3-day buffer catches articles in the gap if a run gets missed. The `curated-history.md` dedupe prevents re-sampling content from prior runs, so the wider window doesn't risk duplicates — it only widens the catch on missed-run weeks.
- **Cadence: weekly.** Audience curator is intended to be run once per week. If a run is invoked off-cadence, that's fine — the curated-history dedupe handles overlap.
- **Selection target: top 15.** Output the top 15 after relevance scoring and theme clustering. If fewer than 15 relevant items exist in the candidate pool, output what you have; don't pad with weak items.

## Guardrails

- Do not modify the source list file at any point.
- Do not modify any file outside the curation output folder, with one exception: `curated-history.md` in the curator folder, which the agent appends to after each successful run.
- Do not access external services requiring authentication. No Inoreader API. No email. No posting anywhere.
- Only read from the public web via standard HTTP requests for RSS feed URLs and article URLs found in those feeds.
- Do not install software or modify system configuration without explicit approval.
- All bash commands get proposed for approval before execution. No silent execution.

## Scope boundaries (out of scope for v0.1)

- No autonomous or scheduled runs.
- No posting anywhere — Substack, LinkedIn, X, anywhere.
- No persistent state across runs except `curated-history.md` (see State tracking below). Each run is otherwise independent.
- No integration with Substack, LinkedIn, or any other downstream tool.
- No installation of system tools without approval.

When Greg asks for something out of scope, say so explicitly. Describe what would need to change to bring it in scope. Don't quietly attempt it.

## State tracking

The agent maintains two persistent state files in the curator folder:

### `curated-history.md` — URL de-duplication

Records URLs included in each day's curation, structured by date.

**Read:** before scoring candidates. URLs in `curated-history.md` are filtered out of the candidate pool. Re-curation is now actively prevented by this file, not passively prevented by the time window. The window still matters for relevance freshness; the history matters for de-duplication.

**Append:** after a successful run, the agent appends today's curated URLs under a new `## YYYY-MM-DD` heading. If the file doesn't exist, create it.

**Override pattern:** when Greg explicitly names a URL to re-surface in a run (e.g., "re-surface the judge layer piece" or "include the Codex bottleneck article again"), include it. Mark the item in the output with `Re-surfaced from [original curation date]:` so the re-surface is visible to anyone reading the file. The override applies only to URLs Greg names explicitly — the default is to skip.

### `feed-stats.md` — per-feed productivity

Records per-feed counts (items in window, items selected) per run. Used to compute a rolling 4 / 8 / 12-run + all-time productivity table included in each curation file. Informs source pruning decisions over time.

**Format:** date-stamped sections, one line per feed:

```
## YYYY-MM-DD
- feed_url | feed_name | in_window | selected
```

Keyed on feed URL (stable across `## ` header renames in `sources/audience.md`). Display name is read from the current source list at run time, not from this file — so renaming a feed in the source list updates its display in future runs without breaking historical data.

**Read:** before writing the curation file, to compute the rolling stats table.

**Append:** as the final write of the run, after the curation file and after `curated-history.md`. If the file doesn't exist, create it (YAML header + title + format note, then the first date section).

**Pruning heuristic:** roughly 12 consecutive runs (3 months at weekly cadence) of zero contribution to keepers = candidate for cull. Discretion overrides the heuristic — a sporadic publisher who lands a high-signal piece once a quarter still earns the slot. Don't auto-prune.

## Implementation expectations

These are how the agent should approach the work, not strict rules:

- **Parse the markdown source list** by reading lines that start with `- url:` under each `## ` header. The URL is the value after `url:`. Other fields (`author:`, `added:`, `why:`) are audit trail for Greg — ignore them.
- **Fetch each RSS feed** via standard HTTP. Handle failures gracefully — log them to the Notes section, skip the feed, don't halt the run.
- **Filter items** to the configured time window before scoring relevance, to avoid wasting reasoning on stale items.
- **Fetch article URLs** when feeds don't include full article text and the title + summary aren't enough to score relevance confidently. Don't fetch every URL by default — fetch when needed.
- **Apply relevance criteria via reasoning**, not keyword matching. The criteria live in `curation-criteria.md`.
- **Cluster the top 15 by theme** *after* selection. Themes derive from the actual content of the selected batch, not from a pre-defined list.
- **Draft react/share text last**, after final selection and grouping. Drafting before selection wastes effort on items that won't make the cut.
- **Read `curated-history.md` early in the run**, after parsing the source list but before fetching feeds. Note any explicit re-surface URLs Greg named in the run instruction.
- **Read `feed-stats.md` early in the run**, alongside `curated-history.md`. Used to compute the rolling productivity table that gets included in the curation file output.
- **Filter out already-curated URLs** from the candidate pool right after the time-window filter, before scoring. Re-surface overrides bypass this filter.
- **Track per-feed counts during the run.** Record in-window count after the time-window filter; record selected count after final selection. These get appended to `feed-stats.md` at the end of the run and surfaced in the curation file's productivity table.
- **Append today's URLs to `curated-history.md` and today's per-feed counts to `feed-stats.md`** as the last writes of the run, after the curation markdown is successfully written. Use `## YYYY-MM-DD` headings in both.
- **Be respectful of feed servers.** Reasonable delay between requests. Standard User-Agent. If a feed rate-limits, back off and skip rather than retrying aggressively.
- **For Reddit feeds, start with a browser User-Agent (Safari) rather than the default curator UA.** Reddit's anti-scraping increasingly blocks bot-identifying UAs — runs hitting `r/Claude`, `r/Anthropic`, and `r/ClaudeCode` 403'd on the curator UA on 2026-05-12 but returned 200 with a Safari UA. Logged in `memory.md` under feed reliability as a 2026-05-12 observation.
- **Classify access per candidate item.** When you read an RSS payload or fetch an article URL, note whether the content is `full` (full article text accessible), `preview` (truncated teaser, "subscribe to read more" splash, or first-N-words excerpt), or `blocked` (login/paywall page in place of the article body, or a 401/403 status). Score on whatever text you do have — preview and blocked items can still be relevant — but log the constraint. Items classified `preview` or `blocked` get surfaced item-by-item in the Notes section of the curation file (see `output-format.md`). Multi-run patterns (a feed that's consistently preview or blocked) get accumulated in `memory.md` under feed reliability, same discipline as other calibrations.

## Run flow (what to report back)

When you run, tell Greg:

1. The source list path you read and the count of feeds in it
2. Progress as you fetch (every few feeds, e.g., "processing feed 5 of 10")
3. The final count of articles reviewed and the count selected for the top 15
4. The output file path so Greg can open it directly

Errors and skipped feeds get logged to the Notes section at the bottom of the markdown file, not just to the chat. The Notes section is the durable record of run anomalies.

## When something goes wrong

- **Source list file missing or unreadable:** Stop the run. Tell Greg the path and the error. Don't guess at a fallback.
- **All feeds fail:** Stop the run. Tell Greg. There's no useful output from a run with zero successful feed fetches.
- **Some feeds fail:** Continue. Log to Notes. Run on the feeds that succeeded.
- **Fewer than 15 relevant articles in the candidate pool:** Output what you have. Don't pad with weak items to hit fifteen. The brand voice rule is "ammunition, not filler."
- **Output folder doesn't exist:** Create it.
- **Output file already exists for today's date:** Ask Greg before overwriting. He may want to keep the prior run.
- **`curated-history.md` missing:** Create it (YAML header + title only). Continue the run.
- **`curated-history.md` malformed:** Stop the run. Tell Greg. Don't overwrite a malformed file — it's the record of what's been curated and corruption shouldn't propagate.
- **`feed-stats.md` missing:** Create it (YAML header + title + format note). Continue the run. The productivity table in the output will reflect "this is the first tracked run."
- **`feed-stats.md` malformed:** Stop the run. Tell Greg. Same principle as `curated-history.md` — corruption shouldn't propagate.
