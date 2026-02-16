---
name: mom6-tracers
description: This skill should be used when users ask about tracers in MOM6; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MOM6: Tracers

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` before using commands below so `docs/`, `.testing/`, `config_src/`, and `src/` paths resolve.

## High-Signal Playbook
### Route conditions
- Use this skill for tracer package selection/configuration (passive, boundary impulse, NW2, MARBL), tracer initialization/restart behavior, and offline tracer stepping (`docs/tracers.rst`, `src/tracer/nw2_tracers.F90`, `src/tracer/MARBL_tracers.F90`, `src/tracer/boundary_impulse_tracer.F90`, `src/tracer/MOM_offline_main.F90`).
- Route to `mom6-working-with-mom6` for end-to-end run orchestration.
- Route to `mom6-theory-and-methods` for EOS/equation interpretation that is not tracer-package-specific.
- Route to `mom6-advanced-topics` for generic forcing/build/parallel testing context.

### Triage questions
1. Which tracer package is in scope (`nw2_tracers`, `boundary_impulse_tracer`, `MARBL_tracers`, offline transport)?
2. Is this a fresh run or restart continuation?
3. Are you in Boussinesq mode (required by NW2 package)?
4. Are forcing files (MARBL IC, river, d14c, restoring) available and correctly pathed?
5. Do you need coupler-exposed tracer fields or internal-only tracers?
6. Which diagnostic confirms success (stocks, checksums, restart reproducibility)?

### Canonical workflow
1. Start from `docs/tracers.rst` to identify the relevant tracer process class.
2. Map that process to concrete source module(s) in `src/tracer/`.
3. Confirm runtime parameter names/defaults in module `get_param` blocks.
4. Configure initialization and restart policy first, then forcing files/timescales.
5. Run short tests and verify tracer diagnostics/stocks before long integrations.
6. If transport behavior is unclear, inspect `MOM_offline_main.F90` and interface-height utilities.

### Minimal working example
```text
# Parameter names from src/tracer/nw2_tracers.F90 and src/tracer/boundary_impulse_tracer.F90
NW2_TRACER_GROUPS = 3
NW2_TRACER_RESTORE_TIMESCALE = 365., 730., 1460.
IMPULSE_SOURCE_TIME = 31536000.0
TRACERS_MAY_REINIT = .false.
```

```text
# Parameter names from src/tracer/MARBL_tracers.F90
MARBL_SETTINGS_FILE = "marbl_in"
MARBL_TRACERS_IC_FILE = "ecosys_jan_IC_omip_latlon_1x1_180W_c230331.nc"
MARBL_TRACERS_MAY_REINIT = .false.
READ_RIV_FLUXES = .true.
MARBL_TRACER_RESTORING_SOURCE = "none"
```

### Pitfalls and fixes
- NW2 tracer initialization aborts outside Boussinesq mode (`src/tracer/nw2_tracers.F90`).
- Restarted runs fail if tracers are missing and `*_MAY_REINIT` is false (`src/tracer/boundary_impulse_tracer.F90`, `src/tracer/MARBL_tracers.F90`).
- `USE_ICE_CATEGORIES=.true.` without `ICE_NCAT>0` is fatal in MARBL setup (`src/tracer/MARBL_tracers.F90`).
- Relative MARBL forcing file names require correct `INPUTDIR` resolution (`src/tracer/MARBL_tracers.F90`).
- Boundary impulse source automatically transitions to sink after `IMPULSE_SOURCE_TIME` (`src/tracer/boundary_impulse_tracer.F90`).
- Tracer restoring behavior differs by source (`none` vs `file`) and timescale source settings (`src/tracer/MARBL_tracers.F90`).

### Convergence and validation checks
- Tracer stocks/checksums are stable over short regression windows.
- Restart/no-restart tracer fields are consistent within expected tolerances.
- Restoration timescale changes produce monotonic damping-rate changes.
- No fatal startup warnings from tracer package parameter parsing.

### Source-code entry links (when docs are insufficient)
- `src/tracer/nw2_tracers.F90`: NeverWorld2 ideal tracer registration, init, and restoring.
- `src/tracer/MARBL_tracers.F90`: MARBL package configuration, forcing inputs, and diagnostics.
- `src/tracer/boundary_impulse_tracer.F90`: boundary impulse source/sink and stock diagnostics.
- `src/tracer/MOM_offline_main.F90`: offline tracer advection/ALE coupling logic.
- `src/core/MOM_interface_heights.F90`: thickness-to-depth conversions used by tracer modules.
- `src/core/MOM_open_boundary.F90`: OBC tracer field handling and reservoirs.
- `src/core/MOM_boundary_update.F90`: time-varying OBC tracer data updates.
- `src/framework/MOM_domains.F90`: domain/halo communication used by tracer operations.

## Scope
- Handle questions about documentation grouped under the 'tracers' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/tracers.rst`

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
- `src/tracer/nw2_tracers.F90`
- `src/tracer/MARBL_tracers.F90`
- `src/tracer/boundary_impulse_tracer.F90`
- `src/tracer/MOM_offline_main.F90`
- `src/core/MOM_interface_heights.F90`
- `src/core/MOM_open_boundary.F90`
- `src/core/MOM_boundary_update.F90`
- `src/framework/MOM_domains.F90`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" config_src pkg src`).
