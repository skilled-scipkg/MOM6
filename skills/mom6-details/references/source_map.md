# MOM6 source map: Details

Generated from source roots:
- `config_src`
- `pkg`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `details`
- `doxygen`
- `sphinx`
- `latex`
- `mathjax`
- `reference`
- `label`
- `anchor`
- `caption`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" config_src pkg src`
- `rg -n "!>|\\\\ref|\\\\eqref|\\\\anchor|\\\\image|\\\\f\\$" src`
- `rg -n "^(\\s*)(subroutine|function)\\s+<name>" <candidate_file>`
- Start by locating the exact warning-producing comment block, then inspect the nearest routine declaration.

## Suggested source entry points (function-level checks)
- `src/user/user_initialization.F90` | anchors: `USER_set_coord`, `USER_init_temperature_salinity`, `write_user_log` | use as concise examples for user-facing routine docs.
- `src/user/user_revise_forcing.F90` | anchors: `user_revise_forcing_init`, `user_alter_forcing` | use for short, high-signal comment and argument-doc patterns.
- `src/user/user_change_diffusivity.F90` | anchors: `user_change_diff_init`, `user_change_diff`, `range_OK` | use for mixed subroutine/function docs and argument annotations.
- `src/core/MOM_open_boundary.F90` | anchors: `open_boundary_config`, `parse_segment_manifest_str`, `parse_segment_data_str` | use for large-module reference/caption/tag troubleshooting.
- `src/core/MOM_boundary_update.F90` | anchors: `call_OBC_register`, `update_OBC_data`, `OBC_register_end` | use for registration/update sequence docs checks.
- `src/core/MOM_interface_heights.F90` | anchors: `find_eta_3d`, `calc_derived_thermo`, `thickness_to_dz_3d` | use for equation-heavy comment formatting checks.
- `src/parameterizations/lateral/MOM_MEKE.F90` | anchors: `step_forward_MEKE`, `ML_MEKE_calculate_features`, `predict_MEKE` | use for argument-doc quality and warning reproduction checks.
- `src/ALE/regrid_solvers.F90` | anchors: `solve_linear_system`, `solve_tridiagonal_system`, `solve_diag_dominant_tridiag` | use for compact equation/procedure doc checks.
