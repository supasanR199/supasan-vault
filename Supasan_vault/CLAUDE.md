# LLM Wiki Schema — Data Engineering Knowledge Base

## Purpose
Personal wiki for BOI STEM++ Advanced Data Engineering and Applied Analytics course notes, built incrementally as course material is processed.

## Directory Structure
```
raw/          — source documents (immutable, read-only)
wiki/
  sources/    — one page per source document (summaries)
  concepts/   — concept/topic pages (entities, patterns, frameworks)
  index.md    — catalog of all wiki pages
  log.md      — append-only operation log
CLAUDE.md     — this file (schema + workflows)
```

## Workflows

### Ingest a new source
1. Read the source document
2. Discuss key takeaways with user (optional)
3. Write `wiki/sources/<slug>.md` — summary page
4. Create or update relevant `wiki/concepts/<slug>.md` pages
5. Update `wiki/index.md` — add new entries
6. Append to `wiki/log.md` — `## [YYYY-MM-DD] ingest | <Title>`

### Answer a query
1. Read `wiki/index.md` to find relevant pages
2. Read those pages
3. Synthesize answer with citations to wiki pages
4. If answer is valuable, file it as a new concept page

### Lint
- Find contradictions between pages
- Find orphan pages (no inbound links)
- Find concepts mentioned but lacking own page
- Check for stale claims

## Page Format

### Source pages (`wiki/sources/`)
```markdown
---
type: source
title: <title>
date_ingested: YYYY-MM-DD
source_file: raw/<filename>
---
## Summary
## Key Concepts
## Notes / Observations
```

### Concept pages (`wiki/concepts/`)
```markdown
---
type: concept
title: <title>
sources: [list of source slugs]
---
## Definition
## Details
## Examples
## Related: [[other-concept]]
```

## Conventions
- Links use Obsidian format: `[[page-name]]`
- Keep English terms exact (Pipeline, Watermark, etc.) — Thai explanations welcome in notes
- Course: BOI STEM++ Advanced Data Engineering, IRIS BrighterBee, Batch 4
- Tool stack mentioned: KNIME, PostgreSQL, REST API, S3
