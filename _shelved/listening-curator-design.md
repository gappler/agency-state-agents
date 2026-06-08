---
title: Listening Curator — Shelved Design
status: shelved
shelved_date: 2026-05-22
shelved_reason: 3-feed pilot too narrow to justify Whisper integration lift, and the broader call (memory entry `curation-expansion-shelved`) closed curation expansion to sibling-media agents entirely. Audience-curator remains the only curator; new publications go into its source list.
revisit_when: substantive change in conditions, not just feed-count growth. Revival requires Greg to reopen the broader curation-expansion question first.
version: 2
---

# Listening Curator — Shelved Design

Sibling agent to audience-curator for podcast curation. Designed but not built. The specific design is preserved here as reference, but the broader project-level decision is that curation expansion to sibling-media agents (listening, youtube, etc.) is closed. See the `curation-expansion-shelved` memory entry for the policy.

Revival of this design specifically would require revisiting that policy, not just adding feeds.

## Pilot scope at park time

Three shows, evaluated and confirmed strong-fit:

- Dwarkesh Podcast — `https://apple.dwarkesh-podcast.workers.dev/feed.rss`
- The Cognitive Revolution — `https://feeds.megaphone.fm/RINTP3108857801`
- This Day in AI — `https://feeds.transistor.fm/this-day-in-ai`

Four shows were evaluated and dropped:

- **Dear Marketers** (Emily Kramer / MKT1) — dead since 2025-08-15 ("season 1 finale" in title).
- **Sharp Tech with Ben Thompson** — paywalled; preview-only in feed. Out of scope per audience-curator's no-auth rule.
- **AI-Driven Marketer (Dan Sanchez)** — directly on theme but sporadic cadence (~47 days between recent episodes). Borderline.
- **Conversations with Tyler** — generalist; AI-relevant episodes infrequent, long episodes mean high transcript cost per low-relevance item.

## Architecture

Structural twin of audience-curator. Same folder layout in `agency-state-agents/listening-curator/`, same `_shared/` dependencies (brand-voice, about-greg), same operational guardrails (no auth, no posting, no installation without approval). Source list at `agency-state-publishing/sources/listening.md`. Output at `curation/[YYYY-MM-DD]-listening.md` (suffix convention already named in audience-curator's AGENT.md).

## Key design decisions

**Dedupe key:** episode `<guid>` rather than URL. Episode page URLs aren't always stable; GUIDs are.

**Two-pass scoring:**
1. **Pass 1 (free):** score relevance on title + show notes only. Surface top 3 candidates.
2. **Pass 2 (~$1–2):** fetch transcripts for the 3 candidates. If the feed includes a `<podcast:transcript>` tag, use it (only This Day in AI has these consistently, ~22% of episodes). Otherwise download audio, send to OpenAI Whisper API, cache at `listening-curator/transcripts/<guid>.txt`.
3. **Final scoring + REACT/SHARE drafting** runs against the transcripts (with show notes as fallback if Whisper fails).

**Selection target:** top 3 with bar. No padding. If only 1 episode clears the bar, output 1.

**Window:** 10 days (matches audience-curator).

**Cadence:** weekly (matches audience-curator).

## Whisper integration

- Service: OpenAI Whisper API (`whisper-1`, $0.006/min). Hybrid pattern (transcribe only the selected 2–3 episodes per run) keeps cost at ~$1–2/run.
- Auth: requires `OPENAI_API_KEY` env var. Surface to Greg on first run, don't set silently.
- Known constraint: 25 MB upload limit. Long episodes need downsampling via ffmpeg before upload. Check for ffmpeg presence on first run; surface install request to Greg if absent.
- Failure mode: if Whisper fails, fall back to show-notes-only for that item, log to Notes, proceed.
- Cache prevents re-transcription on re-runs. Cost reported in the Notes section each run.

## Output format adaptations

Most of the audience-curator format carries over. Three changes for podcasts:

- **Item header:** `### [Episode title]` — episode title, not article title.
- **Metadata block:** Source (show name), Author (host(s)), Link (episode page URL), Episode date, **Duration**.
- **New: `**Pull quote:**`** — one short on-topic quote from the transcript that anchors the REACT/SHARE drafts. Skipped if no transcript was retrieved.
- REACT/SHARE structure, voice rules, and 50–150 word range stay identical.

## Curation criteria

Same buyer, same bar, same `_shared/about-greg.md`. One podcast-specific note added to `curation-criteria.md`: episodes whose value is "this guest is interesting" without operational substance score lower (the podcast equivalent of the list-shaped-content filter). Same pattern-recognition test applies.

## Out of scope for v0.1 (when built)

- Autonomous/scheduled runs.
- Posting anywhere.
- Local Whisper.cpp (would require system install; reconsidered if revival happens and API cost feels wrong).
- Multi-show theme collation across runs (e.g., "the three takes on Codex this week").
- Per-show prioritization beyond the productivity table.

## Revival checklist (when conditions are met)

1. Confirm the source list has grown or pull-quote pattern is in demand elsewhere.
2. Confirm `OPENAI_API_KEY` is available in environment.
3. Confirm `ffmpeg` is installed (or get explicit install approval).
4. Scaffold `agency-state-agents/listening-curator/` (AGENT.md, memory.md, curated-history.md, feed-stats.md, context/curation-criteria.md, context/operational-rules.md, context/output-format.md, transcripts/ directory).
5. Create `agency-state-publishing/sources/listening.md` with the source list.
6. Run pilot. Validate Whisper cost matches projection. Calibrate.
