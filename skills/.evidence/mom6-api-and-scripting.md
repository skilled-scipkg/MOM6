# Evidence: mom6-api-and-scripting

## Primary docs
- `docs/parameterizations_lateral.rst`
- `docs/details/general.md`
- `docs/details/doxygen_warnings.md`
- `docs/front_page.md`
- `docs/apiref.rst`
- `docs/ncar/front_page.md`
- `docs/api/pages.rst`
- `docs/api/modules.rst`

## Primary source entry points
- `skills/mom6-api-and-scripting/references/doc_map.md`
- `src/parameterizations/lateral/MOM_interface_filter.F90`
- `src/parameterizations/lateral/MOM_Zanna_Bolton.F90`
- `src/parameterizations/lateral/MOM_wave_drag.F90`
- `src/parameterizations/lateral/MOM_tidal_forcing.F90`
- `src/parameterizations/lateral/MOM_thickness_diffuse.F90`
- `src/parameterizations/lateral/MOM_streaming_filter.F90`
- `src/parameterizations/lateral/MOM_spherical_harmonics.F90`
- `src/parameterizations/lateral/MOM_self_attr_load.F90`
- `src/parameterizations/lateral/MOM_mixed_layer_restrat.F90`
- `src/parameterizations/lateral/MOM_MEKE_types.F90`
- `src/parameterizations/lateral/MOM_MEKE.F90`
- `src/parameterizations/lateral/MOM_load_love_numbers.F90`
- `src/parameterizations/lateral/MOM_lateral_mixing_coeffs.F90`
- `src/parameterizations/lateral/MOM_internal_tides.F90`
- `src/parameterizations/lateral/MOM_hor_visc.F90`
- `src/user/MOM_wave_interface.F90`
- `src/core/MOM_interface_heights.F90`
- `src/user/Rossby_front_2d_initialization.F90`
- `src/parameterizations/vertical/MOM_vert_friction.F90`

## Extracted headings
- General troublehshooting (FAQ)
- Tags and References
- equation-
- Latex
- doxygen
- PDF: Contents
- Python
- Debugging
- python3 virtual enviroment
- cd to the docs directory within the MOM6 repo
- Doxygen troubleshooting
- Travis

## Executable command hints
- $ source venv/mom6Doc/bin/activate
- Python provides a way to quickly stand up a private web server for checking documentation. It requires knowledge of

## Warnings and pitfalls
- ERROR: `! Dimension too large`
- The last command may appear to hang.  On error, latex will request input from the keyboard.
- _Discrete_PG.dox:39: warning: Illegal command \f as part of a image
- _Discrete_PG.dox:39: warning: Illegal command \Phi as part of a image
- We also discovered that a warning is generated if unknown is used or the same word is
