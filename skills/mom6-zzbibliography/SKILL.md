---
name: mom6-zzbibliography
description: This skill should be used when users ask about zzbibliography in MOM6; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MOM6: Zzbibliography

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` before using commands below so `docs/`, `.testing/`, `config_src/`, and `src/` paths resolve.

## High-Signal Playbook
### Route conditions
- Use this skill for citation management, bibliography build issues, and mapping cited methods to implementation files (`docs/zzbibliography.rst`, `docs/ocean.bib`, `docs/references.bib`, `docs/zotero.bib`).
- Route to `mom6-theory-and-methods` when the request moves from citation metadata to equation/method interpretation.
- Route to `mom6-api-and-scripting` for broader documentation pipeline/API generation issues.
- Route to `mom6-advanced-topics` for environment/dependency setup questions.

### Triage questions
1. Are you adding a new reference key or fixing unresolved citations?
2. Which bibliography file should own the entry (`ocean.bib`, `references.bib`, `zotero.bib`)?
3. Is the issue in html output, latex/pdf output, or both?
4. Is the citation in RST pages or in doxygen comments converted to RST?
5. Do you need to trace a citation to concrete source modules?

### Canonical workflow
1. Confirm the key exists in one of the three bibliography files used by `docs/zzbibliography.rst`.
2. Add/update citation usage in docs (`:cite:` forms in RST).
3. Rebuild docs and inspect warning logs for unresolved keys.
4. Validate bibliography page output and citation links in html/pdf.
5. If requested, map cited method names to source implementation files.

### Minimal working example
```bibtex
@article{MyMethod2026,
  author = {A. Example and B. Example},
  title = {Example Ocean Method},
  journal = {Ocean Modelling},
  year = {2026}
}
```

```bash
cd docs
make html UPDATEHTMLEQS=Y
make latexpdf >& _build/latex_log.txt
```

### Pitfalls and fixes
- `docs/zotero.bib` is generated; manual edits there are fragile and may be overwritten.
- Missing or misspelled keys show up as unresolved citation warnings during build.
- Bibliography rendering depends on `sphinxcontrib-bibtex` in `docs/requirements.txt`.
- Latex/pdf failures can mask citation problems behind broader build errors.
- Duplicate or inconsistent keys across `.bib` files cause ambiguous maintenance and should be normalized.

### Convergence and validation checks
- `docs/zzbibliography.rst` renders entries from `docs/ocean.bib`, `docs/references.bib`, and `docs/zotero.bib`.
- No unresolved citation warnings in html or latex logs.
- Newly cited keys resolve to visible bibliography entries.
- Cited method references are traceable to at least one implementation file when requested.

### Source-code entry links (when behavior details are requested)
- `src/equation_of_state/MOM_EOS.F90`: EOS method families often referenced in bibliography entries.
- `src/equation_of_state/MOM_EOS_TEOS10.F90`: TEOS-related implementation anchor.
- `src/equation_of_state/MOM_EOS_Roquet_SpV.F90`: Roquet polynomial implementation.
- `src/parameterizations/lateral/MOM_MEKE.F90`: eddy-kinetic-energy parameterization implementation.
- `src/parameterizations/lateral/MOM_thickness_diffuse.F90`: GM/TEM diffusion implementation.
- `src/ALE/regrid_solvers.F90`: ALE/remapping method implementation anchor.
- `src/core/MOM_PressureForce.F90`: pressure-force method implementation.
- `src/tracer/MOM_offline_main.F90`: offline tracer algorithm implementation.

## Scope
- Handle questions about documentation grouped under the 'zzbibliography' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/zzbibliography.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- None discovered.

## Test references
- `.testing`
- `config_src/drivers/timing_tests`
- `config_src/drivers/unit_tests`
- `src/framework/testing`

## Optional deeper inspection
- `config_src`
- `pkg`
- `src`

## Source entry points for unresolved issues
- `src/equation_of_state/MOM_EOS.F90`
- `src/equation_of_state/MOM_EOS_TEOS10.F90`
- `src/equation_of_state/MOM_EOS_Roquet_SpV.F90`
- `src/parameterizations/lateral/MOM_MEKE.F90`
- `src/parameterizations/lateral/MOM_thickness_diffuse.F90`
- `src/ALE/regrid_solvers.F90`
- `src/core/MOM_PressureForce.F90`
- `src/tracer/MOM_offline_main.F90`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" config_src pkg src`).
