# Output Format

Exact markdown structure for the curation file. The file lands in the `curation/` folder in the `agency-state-publishing` repo, named:

`[YYYY-MM-DD]-audience.md`

Create the folder if it doesn't exist. Use today's date in YYYY-MM-DD format. The `-audience` suffix carries the agent identifier so a future sibling curator (e.g., `[YYYY-MM-DD]-listening.md`) can land in the same flat folder without collision.

## Structure

```markdown
# Audience Curation — [YYYY-MM-DD]

Reviewed [N] articles from [M] feeds across the last [W] day(s).

## [Theme 1 — derived from content, not pre-defined]

### [Article title]
- **Source:** [feed name]
- **Author:** [if available]
- **Link:** [URL]
- **Why it's relevant:** [1–2 sentences]

**REACT (50–150 words):**
[Draft reaction in Greg's voice — direct, observational, slightly tired, slightly amused. *Beleaguered* on-brand. *Empower* / *transform* / *unlock* forbidden.]

**SHARE (50–150 words):**
[Draft share framing in Greg's voice — adds Greg's angle to the article, not just a summary.]

---

### [Next article in this theme]
...

## [Theme 2]
...

## What's not in the top 15 but worth flagging

[Optional: 2–3 sentences on patterns in the discarded items — vendor announcement clusters, emerging trends, anything worth noticing.]

## Feed productivity

[Rolling per-feed table. See "Feed productivity table" section below for format.]

## Notes

[Logged failures, skipped feeds, anything worth knowing for the next run.]
```

## REACT vs. SHARE — what each is for

These are different drafts for different uses. Don't write the same thing twice.

- **REACT** is Greg's reaction to the piece — what he thinks of it, what's right or wrong about it, what the operational read is. Written for an audience that hasn't necessarily read the article. Standalone commentary.
- **SHARE** is Greg's framing when he passes the article along — the angle that makes it worth someone else's time, not a summary of the article. Written for an audience that's about to click through. Adds value to the link.

If you find yourself writing the same content in both fields, the REACT is probably weak. Make it standalone commentary.

## Voice rules for the drafts

Run every REACT and SHARE through the brand voice self-check before writing. The check lives in `../../_shared/brand-voice.md`. Quick reminders:

- First-person founder voice. *I think*, *I've found*, not *we believe*.
- Direct, observational, slightly tired, slightly amused.
- On-brand: *beleaguered*, *operational sludge*, *method*, *leverage* (as noun), *pipelines*, *workflow*, *outputs*.
- Forbidden: *empower*, *transform*, *unlock*, *amplify*, *scale yourself*, *synergy*, *desktop partner*, *leverage* (as verb), *working systems* (as noun for what gets delivered).
- No fear framing, no overclaim, no fake proof.
- Confident without overclaiming. Warm without being soft.

## Theme naming

Themes are derived from the actual content of the batch, not pre-defined. Name them concretely, not categorically. *"Practitioners pushing back on AI workflow hype"* beats *"AI in marketing"*. Theme names should themselves feel like they could come out of Greg's mouth.

If a batch only produces one or two themes naturally, that's fine — don't force three. If it produces six, see if a few collapse into broader, sharper themes before splitting fifteen items across six small piles.

## Item ordering

Within a theme, lead with the strongest item — the one most worth the senior strategist's attention. Don't alphabetize. Don't order by source. Order by usefulness to the reader.

## Notes section

The Notes section is for what didn't work — failed feeds, skipped articles, edge cases worth flagging for the next run. Format:

```
- Feed [name] returned 404. Skipped.
- Feed [name] returned malformed XML. Skipped.
- [N] articles in the candidate pool but not in top 15 — see "What's not in the top 15" above for patterns.
- [Anything else worth knowing]
```

If the run was clean, the Notes section can be a single line: *Run completed without errors.*

## Feed productivity table

Surfaced near the end of the file (between "What's not in the top 15" and "Notes") so Greg can see source-mix health at a glance and inform pruning decisions over time.

Format: one row per feed in the current `sources/audience.md`. Columns show `selected / in_window` for rolling 4-run, 8-run, 12-run, and all-time spans. Data comes from `audience-curator/feed-stats.md`; the agent appends today's row to that file as the last write of the run.

```markdown
## Feed productivity

| Feed | Last 4 (sel/in) | Last 8 (sel/in) | Last 12 (sel/in) | All-time (sel/in) |
|---|---|---|---|---|
| [Feed name from current source list] | N/N | N/N | N/N | N/N |
| ... |
```

Notes on the table:

- Feed names come from the current `## ` headers in `sources/audience.md` (not from historical data in `feed-stats.md`), so renaming a feed updates its display without breaking history.
- Feeds appear in the table in the order they appear in `sources/audience.md`.
- If a feed was added partway through the tracked history, columns covering pre-add runs show what the system has — the math doesn't pretend the feed was there longer than it was.
- If a feed has been removed from the current `sources/audience.md`, it does *not* appear in the table. The full history remains in `feed-stats.md`.
- When fewer than 4 / 8 / 12 runs of history exist, columns equal what's available. A single-run history shows the same numbers in all four columns. That's honest, not a bug.

Below the table, optional one-line flags for any feed that looks like it's heading toward the 12-run cull threshold (~3 months of zero contribution). Don't auto-prune — just surface the signal.
