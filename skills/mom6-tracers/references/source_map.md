# MOM6 source map: Tracers

Generated from source roots:
- `config_src`
- `pkg`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `tracer`
- `offline`
- `MARBL`
- `nw2`
- `boundary impulse`
- `restart`
- `stock`
- `restore`
- `advection`
- `diffusion`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" config_src pkg src`
- `rg -n "MAY_REINIT|RESTORE|TRACER|MARBL|NW2|IMPULSE" src/tracer/*.F90`
- `rg -n "^(\\s*)(subroutine|function)\\s+<name>" src/tracer/*.F90 src/core/MOM_*boundary*.F90`
- Validate behavior by running `make -C .testing -j test.restart` after tracer/restart changes.

## Suggested source entry points (function-level checks)
- `src/tracer/MOM_tracer_flow_control.F90` | anchors: `tracer_flow_control_init`, `call_tracer_column_fns`, `call_tracer_stocks` | use for tracer package orchestration checks.
- `src/tracer/MOM_tracer_registry.F90` | anchors: `register_tracer`, `register_tracer_diagnostics`, `tracer_Reg_chksum` | use for tracer registration/diagnostic/checksum checks.
- `src/tracer/MOM_tracer_advect.F90` | anchors: `tracer_advect_init`, `advect_tracer`, `advect_x` | use for horizontal tracer advection behavior checks.
- `src/tracer/MOM_tracer_diabatic.F90` | anchors: `tracer_vertdiff`, `tracer_vertdiff_Eulerian`, `applyTracerBoundaryFluxesInOut` | use for vertical diffusion/boundary flux checks.
- `src/tracer/MOM_tracer_hor_diff.F90` | anchors: `tracer_hor_diff_init`, `tracer_hordiff`, `tracer_epipycnal_ML_diff` | use for lateral tracer diffusion checks.
- `src/tracer/nw2_tracers.F90` | anchors: `initialize_nw2_tracers`, `nw2_tracer_column_physics`, `nw2_tracers_end` | use for NeverWorld2 tracer setup/restoring checks.
- `src/tracer/MARBL_tracers.F90` | anchors: `configure_MARBL_tracers`, `initialize_MARBL_tracers`, `MARBL_tracers_column_physics` | use for MARBL package setup/forcing checks.
- `src/tracer/boundary_impulse_tracer.F90` | anchors: `register_boundary_impulse_tracer`, `initialize_boundary_impulse_tracer`, `boundary_impulse_tracer_column_physics` | use for impulse-source timing and stock checks.
- `src/tracer/dyed_obc_tracer.F90` | anchors: `register_dyed_obc_tracer`, `initialize_dyed_obc_tracer`, `dyed_obc_tracer_column_physics` | use for dyed open-boundary tracer checks.
- `src/tracer/MOM_offline_main.F90` | anchors: `offline_transport_init`, `offline_advection_ale`, `offline_diabatic_ale` | use for offline transport stepping checks.
- `src/core/MOM_open_boundary.F90` | anchors: `open_boundary_config`, `parse_for_tracer_reservoirs`, `initialize_obc_tides` | use for OBC tracer field and reservoir checks.
- `src/core/MOM_boundary_update.F90` | anchors: `call_OBC_register`, `update_OBC_data` | use for time-varying OBC tracer update checks.
