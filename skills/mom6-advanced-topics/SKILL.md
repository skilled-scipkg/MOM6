---
name: mom6-advanced-topics
description: This skill should be used when users ask about niche or previously one-doc MOM6 topics that were consolidated to reduce routing noise; it remains docs-first and escalates to targeted source entry points only when needed.
---

# MOM6: Advanced Topics

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` before using commands below so `docs/`, `.testing/`, `config_src/`, and `src/` paths resolve.

## Scope
- Consolidated router for low-frequency topics that previously existed as one-doc skills.
- Use this skill when the request is specific but does not cleanly map to the enriched core skills.

## Collapsed topic routing
- `about`: `docs/about.rst`
- `analysis-and-output`: `docs/details/postProcessEquations.md`
- `build-and-install`: `.testing/README.rst`
- `code-organization`: `docs/code_organization.rst`
- `discrete-space`: `docs/discrete_space.rst`
- `discrete-time`: `docs/discrete_time.rst`
- `forcing`: `docs/forcing.rst`
- `general`: `docs/index.rst`
- `getting-started`: `docs/README.md`
- `grids`: `docs/grids.rst`
- `inputs-and-modeling`: `docs/parameterizations_vertical.rst`
- `other-physics`: `docs/other_physics.rst`
- `parallel-hpc`: `docs/parallel.rst`
- `parameterizations`: `docs/parameterizations.rst`
- `requirements`: `docs/requirements.txt`
- `testing`: `docs/testing.rst`

## Workflow
- Start with the route map above and answer from the mapped primary doc.
- If detail is missing, inspect `references/doc_map.md` for merged inventory context.
- If behavior is still ambiguous, inspect `references/source_map.md` and begin with the targeted source entry links.
- Cite exact documentation/source paths in responses.

## Simulation startup quickplay
```bash
make -C .testing -j build.unit run.unit
make -C .testing -j test.grid
make -C .testing -j test.layout
```
Required inputs:
Use test-case `INPUT/` datasets required by selected `.testing/tc*` cases before running longer integration tests.
Validation checkpoints:
`build.unit` and `run.unit` pass; `test.grid` and `test.layout` complete without FATAL; restart-sensitive changes are followed by `make -C .testing -j test.restart`.

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
- `config_src/drivers/solo_driver/MOM_driver.F90`
- `src/framework/MOM_domains.F90`
- `config_src/infra/FMS2/MOM_time_manager.F90`
- `src/core/MOM_forcing_type.F90`
- `src/diagnostics/MOM_sum_output.F90`
- `src/diagnostics/MOM_harmonic_analysis.F90`
- `src/parameterizations/vertical/MOM_vert_friction.F90`
- `src/parameterizations/lateral/MOM_interface_filter.F90`
- `config_src/external/stochastic_physics/stochastic_physics.F90`
- `src/core/MOM_check_scaling.F90`
- `src/framework/MOM_unit_testing.F90`
- `config_src/drivers/unit_tests/test_numerical_testing_type.F90`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" config_src pkg src`).
