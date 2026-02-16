# MOM6 source map: Advanced Topics

Generated from source roots:
- `config_src`
- `pkg`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `about`
- `analysis`
- `build`
- `code organization`
- `discrete`
- `forcing`
- `grid`
- `parallel`
- `parameterization`
- `requirements`
- `testing`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" config_src pkg src`
- `rg -n "^(\\s*)(subroutine|function)\\s+<name>" <candidate_file>`
- `rg -n "LAYOUT|MASKTABLE|EQN_OF_STATE|TFREEZE_FORM|NONBLOCKING_UPDATES|USE_.*OBC" config_src src`
- If a doc topic maps to a named module, inspect that module first and then its direct call sites.

## Suggested source entry points (function-level checks)
- `config_src/drivers/solo_driver/MOM_driver.F90` | anchors: `initialize_ocean_only_ensembles`, `write_ocean_solo_res` | use for driver lifecycle/restart-output checks.
- `src/framework/MOM_domains.F90` | anchors: `MOM_domains_init`, `MOM_define_layout`, `gen_auto_mask_table` | use for grid/layout behavior and mask-table generation checks.
- `config_src/infra/FMS2/MOM_time_manager.F90` | anchor: `real_to_time` | use for time conversion behavior in FMS2 builds.
- `config_src/infra/FMS1/MOM_time_manager.F90` | anchor: `real_to_time` | use for time conversion behavior in FMS1 builds.
- `src/core/MOM_forcing_type.F90` | anchors: `extractFluxes2d`, `calculateBuoyancyFlux2d`, `find_ustar_fluxes` | use for forcing/buoyancy pathway checks.
- `src/user/user_revise_forcing.F90` | anchors: `user_revise_forcing_init`, `user_alter_forcing` | use for user forcing hooks and perturbation checks.
- `src/diagnostics/MOM_sum_output.F90` | anchors: `MOM_sum_output_init`, `write_energy`, `accumulate_net_input` | use for diagnostic consistency checks.
- `src/diagnostics/MOM_harmonic_analysis.F90` | anchors: `HA_init`, `HA_accum`, `HA_write` | use for spectral/harmonic output checks.
- `src/parameterizations/vertical/MOM_vert_friction.F90` | anchors: `vertvisc_init`, `vertvisc`, `vertvisc_end` | use for vertical-mixing/friction behavior checks.
- `src/parameterizations/vertical/MOM_internal_tide_input.F90` | anchors: `int_tide_input_init`, `set_int_tide_input`, `get_input_TKE` | use for internal-tide forcing checks.
- `src/parameterizations/lateral/MOM_interface_filter.F90` | anchors: `interface_filter_init`, `interface_filter` | use for interface-filter diffusion pathway checks.
- `config_src/external/stochastic_physics/stochastic_physics.F90` | anchors: `init_stochastic_physics_ocn`, `run_stochastic_physics_ocn` | use for stochastic-physics coupling checks.
- `src/core/MOM_check_scaling.F90` | anchors: `check_MOM6_scaling_factors`, `add_scaling` | use for scaling/invariance checks across dimensions.
- `src/framework/MOM_unit_testing.F90` | anchors: `create_test_suite`, `run_test_suite` | use for unit-test harness behavior checks.
- `config_src/drivers/unit_tests/test_numerical_testing_type.F90` | anchor: `program test_numerical_testing_type` | use for numerical testing harness smoke checks.
