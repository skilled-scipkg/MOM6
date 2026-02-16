# MOM6 source map: Working With Mom6

Generated from source roots:
- `config_src`
- `pkg`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `driver`
- `run`
- `restart`
- `layout`
- `domain`
- `open boundary`
- `forcing`
- `offline`
- `diagnostics`
- `unit test`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" config_src pkg src`
- `rg -n "^(\\s*)(subroutine|function)\\s+<name>" config_src/drivers/**/*.F90 src/framework/*.F90 src/core/*.F90`
- `rg -n "restart|layout|OBC|initialize|update" config_src/drivers src/framework src/core src/user`
- Validate workflow behavior with `make -C .testing -j test.grid test.layout test.restart`.

## Suggested source entry points (function-level checks)
- `config_src/drivers/solo_driver/MOM_driver.F90` | anchors: `initialize_ocean_only_ensembles`, `write_ocean_solo_res`, `write_time_stamp_file` | use for ocean-only startup/restart-output checks.
- `config_src/drivers/FMS_cap/ocean_model_MOM.F90` | anchors: `ocean_model_init`, `update_ocean_model`, `ocean_model_save_restart` | use for coupled-cap lifecycle checks.
- `config_src/drivers/nuopc_cap/mom_cap_methods.F90` | anchors: `mom_import`, `mom_export`, `State_SetExport` | use for NUOPC import/export coupling checks.
- `src/framework/MOM_domains.F90` | anchors: `MOM_domains_init`, `MOM_define_layout`, `gen_auto_mask_table` | use for decomposition/layout behavior checks.
- `src/core/MOM_open_boundary.F90` | anchors: `open_boundary_config`, `setup_u_point_obc`, `setup_v_point_obc` | use for OBC configuration checks.
- `src/core/MOM_boundary_update.F90` | anchors: `call_OBC_register`, `update_OBC_data` | use for OBC update timing checks.
- `src/user/user_initialization.F90` | anchors: `USER_initialize_topography`, `USER_initialize_velocity`, `USER_set_OBC_data` | use for user initialization extension checks.
- `src/user/user_revise_forcing.F90` | anchors: `user_revise_forcing_init`, `user_alter_forcing` | use for forcing-adjustment hook checks.
- `src/tracer/MOM_offline_main.F90` | anchors: `offline_transport_init`, `offline_advection_ale`, `update_offline_fields` | use for offline-transport workflow checks.
- `src/ALE/regrid_solvers.F90` | anchors: `solve_linear_system`, `solve_tridiagonal_system`, `solve_diag_dominant_tridiag` | use for ALE/remapping solver behavior checks.
- `src/diagnostics/MOM_sum_output.F90` | anchors: `MOM_sum_output_init`, `write_energy`, `read_depth_list` | use for run-output diagnostics checks.
- `src/framework/MOM_unit_testing.F90` | anchors: `create_test_suite`, `add_unit_test_basic`, `run_test_suite` | use for unit-test harness behavior checks.
- `config_src/drivers/unit_tests/test_numerical_testing_type.F90` | anchor: `program test_numerical_testing_type` | use for numerical test harness smoke checks.
