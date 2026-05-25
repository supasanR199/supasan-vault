---
type: concept
title: Concepts Overview — How the 3 Frameworks Connect
sources: [BOI-STEM-Day1]
---

## Definition

Visual map of how the 3 Day 1 concepts relate and sequence in a real pipeline project.

## Flowchart

```mermaid
flowchart LR
    A([New Pipeline Project]) --> B[Repository Blueprint\nSet up structure first]
    B --> C[Pipeline Spec Framework\nAnswer 5 questions]
    C --> D[Data Loading Patterns\nChoose how to load]
    D --> E([Build & Run Pipeline])

    C -- "spec doc lives in /docs" --> B
    D -- "pattern goes in spec doc" --> C
```

## Sequence

1. **Repository Blueprint** — agree on folder structure before writing any code
2. **Pipeline Spec Framework** — answer 5 questions to define the pipeline contract; output saved to `/docs/pipeline_specification.md`
3. **Data Loading Patterns** — Q1/Q2 answers from the spec determine which pattern to use

## Related

- [[repository-blueprint]]
- [[pipeline-spec-framework]]
- [[data-loading-patterns]]
