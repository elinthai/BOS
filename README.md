# BOS — Content Operating System

A content production pipeline: eight Claude Skills, each one stage, all reading
from and writing to a single Google Sheet.

## What's in this repo

- **`BOS_Content_Repository.xlsx`** — reference copy of the shared data store.
  Tabs: `README`, `Content Repository`, `Value Ladder`, `Launch Checklist Log`,
  `Knowledge Log`. The live version is a Google Sheet, shared with the
  pipeline's service account (see `bos-pipeline` below).
- **`skills/`** — the eight pipeline-stage agents, as plain `SKILL.md` files.
  Install by copying a folder into `~/.claude/skills/`, then invoke by name
  or by handing over the input it expects.

| Stage | Skill | Input → Output |
|---|---|---|
| 1 | `bos-research-agent` | niche statement → validated video ideas + competitor data |
| 2 | `bos-script-agent` | a title → production-ready script |
| 3 | `bos-packaging-agent` | a script → titles/thumbnails/hooks + CTR prediction |
| 4 | `bos-launch-agent` | "just uploaded" → 5-task launch checklist |
| 5 | `bos-repurpose-agent` | finished video/transcript → 15-asset distribution set |
| 6 | `bos-revenue-agent` | a piece of content → value-ladder CTA mapping |
| 7 | `bos-analytics-agent` | pasted YouTube Studio data → weekly performance read |
| 8 | `bos-knowledge-agent` | periodic review → logged patterns/learnings |

They hand off in that order: Research → Script → Packaging → Launch →
Repurpose → Revenue → Analytics → Knowledge. None of them invent numbers or
quotes — missing data gets marked `[NEEDS VERIFICATION]` / `[FILL IN]`
instead.

## Related repo

**[bos-pipeline](https://github.com/elinthai/bos-pipeline)** — the Vercel
backend that automates stage 1. A `/api/research-agent` endpoint calls Claude
with the Research Agent's exact prompt and writes validated ideas straight
into the Content Repository sheet, gated behind a shared-secret header.
Currently built and pushed, deployment paused pending a decision on
Anthropic API billing (it's pay-per-use, separate from a claude.ai
subscription). Everything past Research Agent still runs manually via the
skills in this repo.
