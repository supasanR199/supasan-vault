---
type: source
title: "BOI STEM++ Advanced Data Engineering and Applied Analytics for IT and Developer Teams — Day 1"
date_ingested: 2026-05-24
source_file: raw/BOI-STEM-Day1.pdf
course: BOI STEM++ Development Programs (S-Curve industries)
provider: IRIS BrighterBee
batch: 4
---

## Summary

Day 1 covers two foundational theories for building production-grade data pipelines:
1. **Theory 1**: Translating an architecture diagram into discrete, verifiable pipeline tasks — using the Pipeline Spec Framework (5-question card).
2. **Theory 2**: Choosing the right data loading pattern (Full Load, Incremental, Micro-batch, Streaming) based on freshness, volume, cost, and complexity needs.

Supporting material covers Repository Blueprint (project structure standard) and Markdown as the documentation format of choice.

## Key Concepts

- [[pipeline-spec-framework]] — 5 questions before writing any pipeline
- [[repository-blueprint]] — project structure blueprint (file/folder/workflow/docs standard)
- [[data-loading-patterns]] — Full Load, Incremental, Micro-batch, Streaming + Watermark handling
- Markdown (.md) as the standard for Data Engineering docs (lightweight, git-friendly, cross-platform)

## Day 1 Structure

| Part | Topic |
|------|-------|
| Part 1 | Theory 1: Architecture Blueprint → Pipeline Tasks |
| Part 2 | Pipeline Spec Framework + Repository Blueprint + Markdown |
| Part 3 | Theory 2: Data Loading Patterns + Late Event handling |
| Part 3 | Mini Exercise: choose load pattern for given scenarios |

## Tool Stack Mentioned

- **KNIME** — visual workflow tool (the "Workflow" in Repository Blueprint)
- **PostgreSQL** — data warehouse target (`RAW.raw_orders`)
- **S3** — data lake target
- **REST API** — source system type

## Notes / Observations

- Course is in Thai with English technical terms kept exact.
- Pipeline Spec Framework output feeds directly into Day 2 (Data Quality).
- Repository Blueprint analogy: Pipeline = building, Blueprint = architectural plan, KNIME = construction steps, Folder Structure = building components, Logging/Docs = utilities/manual.
- Key insight on streaming: good streaming is not just fast — it must handle late events, support replay, deduplicate, and allow audit.
