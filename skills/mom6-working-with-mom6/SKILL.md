---
name: mom6-working-with-mom6
description: This skill should be used when users ask about working with mom6 in MOM6; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MOM6: Working With Mom6

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` before using commands below so `docs/`, `.testing/`, `config_src/`, and `src/` paths resolve.

## High-Signal Playbook
### Route conditions
- Use this skill for practical run workflows: driver selection, test/smoke execution, restart loops, diagnostics checks, and transition from docs to code (`docs/working_with_MOM6.rst`, `docs/code_organization.rst`, `.testing/README.rst`).
- Route to `mom6-tracers` for tracer package setup details.
- Route to `mom6-api-and-scripting` for doxygen API navigation issues.
- Route to `mom6-theory-and-methods` for equation/EOS interpretation.
- Route to `mom6-advanced-topics` for parallel/build/forcing/developer-area deep dives.

### Triage questions
1. Ocean-only run (`solo_driver`) or coupled cap workflow (`FMS_cap` / `nuopc_cap`)?
2. Smoke test, reproducibility test, or profiling/regression run?
3. Symmetric or asymmetric grid target?
4. Is open-boundary behavior required?
5. Fresh start or restart continuation?
6. Need offline tracer mode or full prognostic stepping?

### Canonical workflow
1. Choose driver path from `docs/code_organization.rst` (`config_src/drivers/solo_driver` for simplest runs).
2. Build and run a known test target via `.testing/README.rst` before changing physics/code.
3. Validate baseline diagnostics (`ocean.stats`, `chksum_diag`) and restart consistency.
4. Apply minimal user edits in `src/user/*` or OBC wiring in `src/core/*`.
5. Re-run targeted tests (`test.grid`, `test.layout`, `test.restart`) before broader sweeps.
6. Escalate to driver/framework source only when docs and test outputs are insufficient.

### Minimal working example
```bash
make -C .testing -j
make -C .testing -j test.grid
make -C .testing -j test.layout
make -C .testing -j test.restart
```

```bash
# Unit and timing diagnostics from the same harness
make -C .testing -j build.unit run.unit
make -C .testing -j build.timing run.timing
```

### Pitfalls and fixes
- Asymmetric grids do not support open boundary conditions (`.testing/README.rst`).
- Choosing coupled drivers for an ocean-only debugging task adds unnecessary complexity (`docs/code_organization.rst`).
- Forgetting optional external module paths (`config_src/external/*`) can silently alter feature availability (`docs/code_organization.rst`).
- Treating generated API pages as committed files: many are generated during docs build (`docs/working_with_MOM6.rst`).
- Repro tests can fail with aggressive optimization; use recommended flags in test harness docs (`.testing/README.rst`).

### Convergence and validation checks
- `test.grid`, `test.layout`, and `test.restart` are clean for your branch.
- `ocean.stats` and `chksum_diag` are stable across expected-equivalent runs.
- Restart split-run and one-shot run agree.
- Any driver/config edit still passes at least one representative `tc*` case.

### Source-code entry links (when docs are insufficient)
- `config_src/drivers/solo_driver/MOM_driver.F90`: ocean-only driver lifecycle.
- `config_src/drivers/FMS_cap/ocean_model_MOM.F90`: coupler-facing ocean model interface.
- `config_src/drivers/nuopc_cap/mom_cap_methods.F90`: NUOPC cap method wiring.
- `src/framework/MOM_domains.F90`: layout, halos, and communication configuration.
- `src/core/MOM_open_boundary.F90`: open-boundary control and data pathways.
- `src/core/MOM_boundary_update.F90`: OBC registration/update orchestration.
- `src/user/user_initialization.F90`: user initialization extension point.
- `src/user/user_revise_forcing.F90`: user forcing customization hook.
- `src/ALE/regrid_solvers.F90`: remap/regrid internals for vertical motion workflows.
- `src/tracer/MOM_offline_main.F90`: offline tracer stepping path.

## Scope
- Handle questions about documentation grouped under the 'working-with-mom6' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/working_with_MOM6.rst`

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
- `config_src/drivers/solo_driver/MOM_driver.F90`
- `config_src/drivers/FMS_cap/ocean_model_MOM.F90`
- `config_src/drivers/nuopc_cap/mom_cap_methods.F90`
- `src/framework/MOM_domains.F90`
- `src/core/MOM_open_boundary.F90`
- `src/core/MOM_boundary_update.F90`
- `src/user/user_initialization.F90`
- `src/user/user_revise_forcing.F90`
- `src/ALE/regrid_solvers.F90`
- `src/tracer/MOM_offline_main.F90`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" config_src pkg src`).
