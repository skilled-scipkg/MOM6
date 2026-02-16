---
name: mom6-api-and-scripting
description: This skill should be used when users ask about api and scripting in MOM6; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MOM6: API and Scripting

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` before using commands below so `docs/`, `.testing/`, `config_src/`, and `src/` paths resolve.

## High-Signal Playbook
### Route conditions
- Use this skill for API navigation, doxygen/sphinx API generation, module/page lookup, and scripting around documented interfaces (`docs/front_page.md`, `docs/apiref.rst`, `docs/api/modules.rst`, `docs/api/pages.rst`).
- Route to `mom6-theory-and-methods` for derivations/equations and EOS math.
- Route to `mom6-working-with-mom6` for full run workflows and driver choices.
- Route to `mom6-advanced-topics` for build, parallel, forcing, or broad package topics.

### Triage questions
1. Do you need hosted API docs or a local generated copy?
2. Is the target the NOAA/GFDL tree or NCAR fork docs (`docs/front_page.md` vs `docs/ncar/front_page.md`)?
3. Are you looking for a module, page, or source file path?
4. Is the question about lateral parameterization APIs (`docs/parameterizations_lateral.rst`) or docs tooling errors?
5. Do you already have a symbol name to search in source?

### Canonical workflow
1. Start at `docs/front_page.md` (or `docs/ncar/front_page.md`) to choose the API surface.
2. Use `docs/apiref.rst` and `docs/api/modules.rst` for stable module entry points.
3. Use `docs/api/pages.rst` to locate feature pages when module pages are not enough.
4. If local docs are needed, build API/user docs in `docs/` (commands below).
5. If behavior is still ambiguous, pivot to source entry files under `src/parameterizations/lateral/`.
6. Answer with exact file paths and symbol names.

### Minimal working example
```bash
python3 -m venv venv/mom6Doc
source venv/mom6Doc/bin/activate
cd docs
pip3 install -r requirements.txt
make nortd
make html UPDATEHTMLEQS=Y
python3 -m http.server 8080
# then open http://localhost:8080/
```

```bash
rg -n "MOM_MEKE|MOM_thickness_diffuse|MOM_lateral_mixing_coeffs|MOM_interface_filter" \
  src/parameterizations/lateral
```

### Pitfalls and fixes
- `! Dimension too large` during latex build: reduce graph complexity (for example lower `DOT_GRAPH_MAX_NODES`) and rerun (`docs/details/general.md`).
- `make latexpdf` appears hung: latex may be waiting for input; continue with `R` then Enter (`docs/details/general.md`).
- Image-caption math warnings like illegal `\Phi`: use escaped forms for doxygen image captions (`docs/details/doxygen_warnings.md`).
- Unexpected escapes in generated equations from Python tooling: protect backslashes in strings (for example `\\theta`) (`docs/details/general.md`).
- Assuming generated pages are checked in: `docs/api/generated/*` pages are produced during docs generation (`docs/api/pages.rst`).

### Convergence and validation checks
- `docs/APIs/index.html` exists after `make nortd` and core module/page links resolve (`docs/front_page.md`).
- `docs/_build/html/index.html` exists after `make html` and cross-page equation links are stable when `UPDATEHTMLEQS=Y` (`docs/README.md`).
- `_build/doxygen_warn_rtd_log.txt` has no new critical warnings (`docs/README.md`).
- Selected parameterization in docs maps to an implementation module in `src/parameterizations/lateral/`.

### Source-code entry links (when docs are insufficient)
- `src/parameterizations/lateral/MOM_interface_filter.F90`: interface filtering entry points.
- `src/parameterizations/lateral/MOM_hor_visc.F90`: lateral viscosity implementation hooks.
- `src/parameterizations/lateral/MOM_thickness_diffuse.F90`: GM/TEM and thickness diffusion logic.
- `src/parameterizations/lateral/MOM_lateral_mixing_coeffs.F90`: diffusivity coefficient construction.
- `src/parameterizations/lateral/MOM_MEKE.F90`: mesoscale eddy kinetic energy pathway.
- `src/parameterizations/lateral/MOM_mixed_layer_restrat.F90`: mixed-layer restratification implementation.
- `src/parameterizations/lateral/MOM_tidal_forcing.F90`: tidal forcing injection path.
- `src/parameterizations/lateral/MOM_self_attr_load.F90`: self-attraction and loading calculations.
- `src/core/MOM_interface_heights.F90`: interface/thickness transformations used by parameterizations.
- `src/user/MOM_wave_interface.F90`: user-side wave-coupling interface hooks.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/parameterizations_lateral.rst`
- `docs/details/general.md`
- `docs/details/doxygen_warnings.md`
- `docs/front_page.md`
- `docs/apiref.rst`
- `docs/ncar/front_page.md`
- `docs/api/pages.rst`
- `docs/api/modules.rst`

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
- `src/parameterizations/lateral/MOM_interface_filter.F90`
- `src/parameterizations/lateral/MOM_hor_visc.F90`
- `src/parameterizations/lateral/MOM_thickness_diffuse.F90`
- `src/parameterizations/lateral/MOM_lateral_mixing_coeffs.F90`
- `src/parameterizations/lateral/MOM_MEKE.F90`
- `src/parameterizations/lateral/MOM_mixed_layer_restrat.F90`
- `src/parameterizations/lateral/MOM_tidal_forcing.F90`
- `src/parameterizations/lateral/MOM_self_attr_load.F90`
- `src/core/MOM_interface_heights.F90`
- `src/user/MOM_wave_interface.F90`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" config_src pkg src`).
