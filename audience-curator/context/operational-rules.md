# Operational Rules

Guardrails, scope boundaries, and the v0.1 first-run caps. These rules are stable — they don't change run-to-run. If they need to change, update this file rather than overriding it in conversation.

## v0.1 first-run caps

For the first run, scope down to confirm cost and runtime shape:

- Process the **first 10 feeds** from the OPML, not all of them
- Use a **1-day window** instead of 3
- Cap **candidate articles at 100** before applying the top-15 selection

Once the first run completes successfully, these caps can be lifted. Greg will tell you when. Until he does, keep the caps in place.

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

The agent maintains one persistent state file: `curated-history.md` in the curator folder. It records URLs included in each day's curation, structured by date.

**Read:** before scoring candidates. URLs in `curated-history.md` are filtered out of the candidate pool. Re-curation is now actively prevented by this file, not passively prevented by the time window. The window still matters for relevance freshness; the history matters for de-duplication.

**Append:** after a successful run, the agent appends today's curated URLs under a new `## YYYY-MM-DD` heading. If the file doesn't exist, create it.

**Override pattern:** when Greg explicitly names a URL to re-surface in a run (e.g., "re-surface the judge layer piece" or "include the Codex bottleneck article again"), include it. Mark the item in the output with `Re-surfaced from [original curation date]:` so the re-surface is visible to anyone reading the file. The override applies only to URLs Greg names explicitly — the default is to skip.

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
- **Filter out already-curated URLs** from the candidate pool right after the time-window filter, before scoring. Re-surface overrides bypass this filter.
- **Append today's URLs to `curated-history.md`** as the last write of the run, after the curation markdown is successfully written. Use a `## YYYY-MM-DD` heading.
- **Be respectful of feed servers.** Reasonable delay between requests. Standard User-Agent. If a feed rate-limits, back off and skip rather than retrying aggressively.
- **For Reddit feeds, start with a browser User-Agent (Safari) rather than the default curator UA.** Reddit's anti-scraping increasingly blocks bot-identifying UAs — runs hitting `r/Claude`, `r/Anthropic`, and `r/ClaudeCode` 403'd on the curator UA on 2026-05-12 but returned 200 with a Safari UA. Logged in `memory.md` under feed reliability as a 2026-05-12 observation.

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
