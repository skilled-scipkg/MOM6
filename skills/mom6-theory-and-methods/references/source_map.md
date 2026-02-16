# MOM6 source map: Theory and Methods

Generated from source roots:
- `config_src`
- `pkg`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `theory`
- `equation`
- `EOS`
- `EQN_OF_STATE`
- `TFREEZE_FORM`
- `pressure force`
- `derivation`
- `method`
- `quadrature`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" config_src pkg src`
- `rg -n "EQN_OF_STATE|TFREEZE_FORM|EOS_QUADRATURE|USE_WRIGHT_2ND_DERIV_BUG" src/equation_of_state/MOM_EOS.F90`
- `rg -n "^(\\s*)(subroutine|function)\\s+<name>" src/equation_of_state/*.F90 src/core/MOM_PressureForce*.F90`
- `make -C .testing -j build.unit run.unit` to validate EOS-method behavior after changes.

## Suggested source entry points (function-level checks)
- `src/equation_of_state/MOM_EOS.F90` | anchors: `calculate_density_scalar`, `calculate_TFreeze_scalar`, `EoS_fit_range` | use for EOS/TFreeze selection and top-level algorithm checks.
- `src/equation_of_state/MOM_EOS_base_type.F90` | anchors: `i_EOS_fit_range`, `a_calculate_density_array`, `a_calculate_spec_vol_array` | use for EOS interface contract checks.
- `src/equation_of_state/MOM_EOS_TEOS10.F90` | anchor: `EoS_fit_range_teos10` | use for TEOS-10 fit-range and implementation sanity checks.
- `src/equation_of_state/MOM_EOS_Wright_full.F90` | anchors: `EoS_fit_range_Wright_full`, `calculate_density_array_Wright_full`, `calculate_spec_vol_array_Wright_full` | use for Wright-full pathway checks.
- `src/equation_of_state/MOM_EOS_linear.F90` | anchors: `set_params_linear`, `calculate_density_array_linear`, `calculate_spec_vol_array_linear` | use for linear EOS parameter/response checks.
- `src/equation_of_state/MOM_EOS_UNESCO.F90` | anchor: `EoS_fit_range_UNESCO` | use for UNESCO fit-range checks.
- `src/equation_of_state/MOM_EOS_Roquet_SpV.F90` | anchors: `EoS_fit_range_Roquet_SpV`, `calculate_density_array_Roquet_SpV`, `calculate_spec_vol_array_Roquet_SpV` | use for Roquet specific-volume pathway checks.
- `src/equation_of_state/MOM_TFreeze.F90` | anchors: `calculate_TFreeze_linear_scalar`, `calculate_TFreeze_Millero_scalar`, `calculate_TFreeze_teos10_scalar` | use for freezing-point formulation checks.
- `src/core/MOM_PressureForce.F90` | anchors: `PressureForce_init`, `PressureForce` | use for pressure-force dispatch checks.
- `src/core/MOM_PressureForce_Montgomery.F90` | anchors: `PressureForce_Mont_init`, `PressureForce_Mont_Bouss`, `PressureForce_Mont_nonBouss` | use for Montgomery-form pressure-force checks.
- `src/core/MOM_PressureForce_FV.F90` | anchors: `PressureForce_FV_init`, `PressureForce_FV_Bouss`, `PressureForce_FV_nonBouss` | use for finite-volume pressure-force checks.
- `config_src/drivers/unit_tests/test_MOM_EOS.F90` | anchor: `program test_MOM_EOS` | use for EOS regression smoke checks.
- `config_src/drivers/timing_tests/time_MOM_EOS.F90` | anchors: `run_suite`, `run_one` | use for method-level timing/performance checks.
