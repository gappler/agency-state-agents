---
title: For Substack Readers — Public Edition
purpose: reader-facing copies of audience-curator files, shared via Substack
version: 1
---

# For Substack Readers

This folder is the **public edition** of the audience-curator — the versions safe to
show Substack readers. The working files the agent actually reads and writes live in the
parent `audience-curator/` folder; these are derived copies, kept here on purpose.

They are **not** auto-synced. When a canonical file changes, the copy here has to be
re-derived by hand, so treat the parent folder as the source of truth and this folder as
a published snapshot.

| File | Relationship to canonical |
|------|---------------------------|
| `audience.md` | Verbatim copy of `../sources/audience.md` (the source list is already public-safe). |
| `memory.md` | **Sanitized** copy of `../memory.md` — internal name, operational workarounds, and dated calibration history removed. Shows the *shape* of the agent's memory without the internal guts. |
| `2026-05-14-audience.md` | A representative sample of curated output. |

If a canonical file gains anything reader-unsafe, update the sanitized copy here before
re-sharing — don't point readers at the parent files directly.
