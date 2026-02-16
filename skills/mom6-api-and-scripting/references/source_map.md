# MOM6 source map: API and Scripting

Generated from source roots:
- `config_src`
- `pkg`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `api`
- `apiref`
- `doxygen`
- `modules`
- `pages`
- `interface`
- `lateral`
- `scripting`
- `wave`
- `MEKE`
- `thickness`
- `mixing`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" config_src pkg src`
- `rg -n "^(\\s*)(subroutine|function)\\s+<name>" src/parameterizations/lateral/*.F90 src/core/*.F90 src/user/*.F90`
- `rg -n "interface_filter|thickness_diffuse|MEKE|SAL|tidal_forcing" src/parameterizations/lateral`
- Start with docs-derived symbol names from `docs/apiref.rst`, then inspect matching implementation routines.

## Suggested source entry points (function-level checks)
- `src/parameterizations/lateral/MOM_interface_filter.F90` | anchors: `interface_filter_init`, `interface_filter`, `filter_interface` | use for interface-filter API behavior checks.
- `src/parameterizations/lateral/MOM_hor_visc.F90` | anchors: `hor_visc_init`, `horizontal_viscosity`, `hor_visc_end` | use for lateral viscosity API/parameter parsing checks.
- `src/parameterizations/lateral/MOM_thickness_diffuse.F90` | anchors: `thickness_diffuse_init`, `thickness_diffuse`, `thickness_diffuse_get_KH` | use for GM/TEM and thickness diffusion API checks.
- `src/parameterizations/lateral/MOM_lateral_mixing_coeffs.F90` | anchors: `calc_slope_functions`, `calc_Eady_growth_rate_2D`, `calc_QG_slopes` | use for coefficient/slope API behavior checks.
- `src/parameterizations/lateral/MOM_MEKE.F90` | anchors: `ML_MEKE_init`, `step_forward_MEKE`, `predict_MEKE` | use for MEKE setup/step/prediction API checks.
- `src/parameterizations/lateral/MOM_mixed_layer_restrat.F90` | anchors: `mixedlayer_restrat`, `mixedlayer_restrat_Bodner`, `detect_mld` | use for restratification API checks.
- `src/parameterizations/lateral/MOM_tidal_forcing.F90` | anchors: `tidal_forcing_init`, `calc_tidal_forcing`, `calc_tidal_forcing_legacy` | use for tidal-forcing API checks.
- `src/parameterizations/lateral/MOM_self_attr_load.F90` | anchors: `SAL_init`, `calc_SAL`, `SAL_end` | use for self-attraction/loading API checks.
- `src/core/MOM_interface_heights.F90` | anchors: `find_eta_3d`, `dz_to_thickness_tv`, `thickness_to_dz_3d` | use for interface-height conversion API checks.
- `src/user/MOM_wave_interface.F90` | anchors: `MOM_wave_interface_init`, `Update_Surface_Waves`, `Update_Stokes_Drift` | use for user-side wave-coupling API checks.
