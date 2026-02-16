---
name: mom6-index
description: This skill should be used when users ask how to use MOM6 and the correct generated documentation skill must be selected before going deeper into source code.
---

# MOM6 Skills Index

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` first so repo paths like `docs/`, `.testing/`, `config_src/`, and `src/` resolve.

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.
- Use enriched core skills first for first-week workflows; use `mom6-advanced-topics` for collapsed niche topics.

## Generated topic skills
- `mom6-api-and-scripting`: API and Scripting (API navigation, docs generation, module/page lookup, scripting interfaces)
- `mom6-theory-and-methods`: Theory and Methods (equations, EOS/TFreeze selection, method-to-code mapping)
- `mom6-details`: Details (doxygen/sphinx/latex/mathjax troubleshooting and formatting edge cases)
- `mom6-working-with-mom6`: Working With MOM6 (driver selection, run/restart workflow, baseline test execution)
- `mom6-tracers`: Tracers (tracer package setup, restart behavior, offline tracer transport)
- `mom6-zzbibliography`: Zzbibliography (citations, bibliography integration, source-method citation mapping)
- `mom6-advanced-topics`: Advanced Topics (collapsed one-doc themes: about, build/install, code organization, discrete space/time, forcing, grids, parameterizations, parallel, requirements, testing, and related niche areas)

## Documentation-first inputs
- `docs`

## Tutorials and examples roots
- `.testing`

## Test roots for behavior checks
- `.testing`
- `config_src/drivers/timing_tests`
- `config_src/drivers/unit_tests`
- `src/framework/testing`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, open `skills/<topic-skill>/references/doc_map.md`.
- If documentation still leaves ambiguity, open `skills/<topic-skill>/references/source_map.md` and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" config_src pkg src`).

## Source directories for deeper inspection
- `config_src`
- `pkg`
- `src`
