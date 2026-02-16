# MOM6 source map: Zzbibliography

Generated from source roots:
- `config_src`
- `pkg`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `citation`
- `bibliography`
- `reference key`
- `EOS`
- `TEOS`
- `Roquet`
- `MEKE`
- `thickness diffusion`
- `ALE`
- `offline transport`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" config_src pkg src`
- `rg -n ":cite:|\\\\cite|@[a-zA-Z]+\\{" docs/zzbibliography.rst docs/*.bib`
- `rg -n "^(\\s*)(subroutine|function)\\s+<name>" src/equation_of_state/*.F90 src/parameterizations/lateral/*.F90 src/core/*.F90`
- For citation-to-code requests, identify method keyword in docs first, then map to the source routine below.

## Suggested source entry points (function-level checks)
- `src/equation_of_state/MOM_EOS.F90` | anchors: `calculate_density_scalar`, `calculate_TFreeze_scalar`, `EoS_fit_range` | use for EOS-method citation mapping.
- `src/equation_of_state/MOM_EOS_TEOS10.F90` | anchor: `EoS_fit_range_teos10` | use for TEOS-specific citation mapping.
- `src/equation_of_state/MOM_EOS_Roquet_SpV.F90` | anchors: `calculate_density_array_Roquet_SpV`, `calculate_spec_vol_array_Roquet_SpV` | use for Roquet polynomial citation mapping.
- `src/equation_of_state/MOM_TFreeze.F90` | anchors: `calculate_TFreeze_Millero_scalar`, `calculate_TFreeze_teos10_scalar` | use for freezing-point method citation mapping.
- `src/core/MOM_PressureForce.F90` | anchors: `PressureForce_init`, `PressureForce` | use for pressure-gradient method citation mapping.
- `src/core/MOM_PressureForce_Montgomery.F90` | anchors: `PressureForce_Mont_init`, `PressureForce_Mont_Bouss` | use for Montgomery-form method citation mapping.
- `src/core/MOM_PressureForce_FV.F90` | anchors: `PressureForce_FV_init`, `PressureForce_FV_Bouss` | use for finite-volume pressure-force citation mapping.
- `src/parameterizations/lateral/MOM_MEKE.F90` | anchors: `step_forward_MEKE`, `MEKE_equilibrium`, `predict_MEKE` | use for MEKE method citation mapping.
- `src/parameterizations/lateral/MOM_thickness_diffuse.F90` | anchors: `thickness_diffuse`, `streamfn_solver`, `thickness_diffuse_init` | use for GM/TEM thickness-diffusion citation mapping.
- `src/ALE/regrid_solvers.F90` | anchors: `solve_linear_system`, `solve_tridiagonal_system`, `solve_diag_dominant_tridiag` | use for ALE/remapping method citation mapping.
- `src/tracer/MOM_offline_main.F90` | anchors: `offline_transport_init`, `offline_advection_ale`, `offline_diabatic_ale` | use for offline-transport citation mapping.
