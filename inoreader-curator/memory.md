# Inoreader Curator — Memory

This file accumulates corrections, learned preferences, and patterns observed across runs. Update it in place when Greg corrects you or you notice something worth remembering. Don't append-only; rewrite sections so they stay coherent.

When in doubt about whether something belongs here vs. in `AGENT.md` or a `context/` file: if it's a learned preference or correction, it goes here. If it's a stable rule, it belongs in `AGENT.md` or `context/`.

---

## Memory discipline

*The bar for writing something to memory. Apply this before adding any new entry below.*

- Memory entries should reflect patterns observed across multiple runs OR explicit corrections from Greg, not single-run observations.
- If something is interesting but not yet a pattern, mention it in chat for that run; don't write it to memory until it recurs or Greg confirms.

---

## Voice corrections

*Specific phrases, words, or framings Greg has corrected in past react/share drafts. When a correction repeats, add it here so it doesn't repeat again.*

(none yet)

---

## Useful framings the agent has surfaced

*Compact phrasings the agent has generated that proved tighter or more useful than the source-file equivalents. Keep so they don't get reinvented or lost.*

- **"Would this make them roll their eyes?"** — the inverse phrasing of the ammunition test. Useful as a negative-case gut-check on voice drafts: if the answer is yes, the line is off-brand even if no forbidden words appear.
- **"Monday morning test"** — for relevance scoring. Would a working strategist be able to do something with this when they sit down at their desk on Monday? If no, score lower. Sharper than the abstract "operationally honest" criterion when cutting borderline items.

---

## Relevance calibration

*When Greg has flagged an article as wrongly included or wrongly excluded, capture the pattern here so future scoring reflects it.*

- **Reddit pattern-level vs. implementation-level (calibrated across 2026-05-04, 2026-05-05, 2026-05-09 runs).** Reddit produced most of the noise across three runs. Practitioner posts that survived translated because the lesson was in the method — "harness your agent," named patterns, the project-complexity threshold question, the knowledge-base-method-through-pain post. Practitioner posts that didn't survive were working through their own bugs, version regressions, billing surprises, or vendor complaints. Same operational credibility on the author side; different *kind* of content. When a Reddit item is borderline, the test is: is this teaching a pattern, or solving an implementation problem? Pattern-level keeps, implementation-level rejects. The disambiguation now lives in `curation-criteria.md`; this entry exists so the calibration history is visible.

- **"Where Claude broke this week" theme produced zero keepers across three runs (2026-05-04, 2026-05-05, 2026-05-09).** Items grouped under this theme — and any operational-bug cluster (version regressions, outage post-mortems, "my agent cost $1000 overnight") — are operational signal for practitioners running Claude Code in production, not for the buyer. The cluster pattern itself is worth surfacing: when these items appear, name the cluster in the "what's not in the top 15 but worth flagging" section so Greg can see the pattern exists. Don't promote individual items into the top 15 on the strength of the theme.

- **Substack runs high-signal in the current feed mix (observed across 2026-05-04, 2026-05-05, 2026-05-09).** Every Nate's Substack item across the three runs was a keep, and the Algorithmic Bridge piece on tool sprawl was a keep. Observation, not instruction: no source quota, no source prior, no balancing. The expectation is that tighter Reddit filtering will let Substack surface naturally on relevance alone. Flag it if the pattern reverses.

---

## Theme clustering preferences

*How Greg likes themes named, sized, or grouped. Patterns observed across runs.*

(none yet)

---

## Feed prioritization

*How to choose which feeds to include when caps or constraints force a cut.*

(none yet — Google News feeds were removed from the OPML on 2026-05-09 because they crowded out more authoritative sources. Greg expects to add more feeds over time; revisit prioritization rules then.)

---

## Feed reliability

*Feeds that consistently fail, return junk, or are otherwise worth flagging. Greg can decide whether to remove them from the OPML based on what accumulates here.*

- **If Google News feeds are added back later, fetch with curl `-L` to follow redirects.** Google News RSS URLs `/news/rss/search?...` 302 to `/rss/search?...`; without `-L`, fetches return 0 bytes silently.

---

## Format preferences

*Small format choices Greg has corrected — heading styles, ordering within items, how the Notes section reads.*

(none yet)

---

## Open questions for Greg

*Things the agent has surfaced but Greg hasn't ruled on yet. Clear out when resolved.*

(none yet)
