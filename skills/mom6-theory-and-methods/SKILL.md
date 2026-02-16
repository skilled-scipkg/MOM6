---
name: mom6-theory-and-methods
description: This skill should be used when users ask about theory and methods in MOM6; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MOM6: Theory and Methods

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` before using commands below so `docs/`, `.testing/`, `config_src/`, and `src/` paths resolve.

## High-Signal Playbook
### Route conditions
- Use this skill for equation-to-code mapping, EOS method selection, freezing-point formulation, and reference-label mechanics (`docs/equations.rst`, `docs/details/doxygen_sphinx_ref.md`).
- Route to `mom6-tracers` for tracer-package-specific runtime choices and transport workflows.
- Route to `mom6-api-and-scripting` for API page generation/navigation questions.
- Route to `mom6-advanced-topics` for parallel/build/testing infrastructure topics.

### Triage questions
1. Do you need physical-method interpretation, or exact implementation location?
2. Which EOS family is intended (`LINEAR`, `WRIGHT_*`, `TEOS10`, `ROQUET_*`, `UNESCO`)?
3. Which freezing form is intended (`LINEAR`, `MILLERO_78`, `TEOS_POLY`, `TEOS10`)?
4. Are model state variables conservative-temp/absolute-salinity or potential-temp/practical-salinity?
5. Is the issue a reference-label/linking problem across pages?

### Canonical workflow
1. Start from `docs/equations.rst` to locate the target equation block or section.
2. For cross-page refs/labels, apply rules from `docs/details/doxygen_sphinx_ref.md`.
3. Map configuration choices to `src/equation_of_state/MOM_EOS.F90` (`EQN_OF_STATE`, `TFREEZE_FORM`, `EOS_QUADRATURE`).
4. Trace implementation in EOS backend modules (`MOM_EOS_TEOS10.F90`, `MOM_EOS_Wright_full.F90`, etc.).
5. Validate with unit tests before claiming behavioral changes.

### Minimal working example
```text
# Runtime parameter sketch (names from src/equation_of_state/MOM_EOS.F90)
EQN_OF_STATE = "TEOS10"
TFREEZE_FORM = "TEOS10"
EOS_QUADRATURE = .true.
TFREEZE_S_IS_PRACS = .false.
TFREEZE_T_IS_POTT = .false.
```

```bash
rg -n "EQN_OF_STATE|TFREEZE_FORM|EOS_QUADRATURE|TFREEZE_S_IS_PRACS|TFREEZE_T_IS_POTT" \
  src/equation_of_state/MOM_EOS.F90
make -C .testing -j build.unit run.unit
```

### Pitfalls and fixes
- Invalid `EQN_OF_STATE` or `TFREEZE_FORM` values are fatal (`src/equation_of_state/MOM_EOS.F90`).
- `TEOS10`/`ROQUET_*` EOS paired with non-TEOS freezing forms generates warnings (`src/equation_of_state/MOM_EOS.F90`).
- Mis-specified salinity/temperature type flags can silently apply wrong conversions (`src/equation_of_state/MOM_EOS.F90`).
- Wright second-derivative compatibility mode (`USE_WRIGHT_2ND_DERIV_BUG`) changes derivative behavior (`src/equation_of_state/MOM_EOS.F90`).
- Eqn labels containing `:` or `_` are normalized in Sphinx; mismatched references fail (`docs/details/doxygen_sphinx_ref.md`).
- Multi-line equation references require the extended `\eqref{tagA,tagB,tagC}` pattern for cross-page links (`docs/details/doxygen_sphinx_ref.md`).

### Convergence and validation checks
- EOS and TFreeze forms are physically consistent and warning-free at startup.
- Unit tests in `config_src/drivers/unit_tests/test_MOM_EOS.F90` pass.
- For changed state ranges, EOS fit-range warnings are absent or explicitly justified.
- Equation and figure references resolve in generated html/pdf docs.

### Source-code entry links (when docs are insufficient)
- `src/equation_of_state/MOM_EOS.F90`: central EOS/TFreeze selection and parameter parsing.
- `src/equation_of_state/MOM_EOS_base_type.F90`: abstract EOS interface and required methods.
- `src/equation_of_state/MOM_EOS_TEOS10.F90`: TEOS-10 implementation path.
- `src/equation_of_state/MOM_EOS_Wright_full.F90`: Wright full EOS implementation.
- `src/equation_of_state/MOM_EOS_Roquet_SpV.F90`: non-Boussinesq specific-volume polynomial EOS.
- `src/equation_of_state/MOM_TFreeze.F90`: freezing-point formulations.
- `src/core/MOM_PressureForce.F90`: pressure-force coupling point.
- `src/core/MOM_PressureForce_Montgomery.F90`: Montgomery-form pressure-force implementation.
- `src/core/MOM_PressureForce_FV.F90`: finite-volume pressure-force variant.
- `config_src/drivers/unit_tests/test_MOM_EOS.F90`: regression/validation anchor for EOS behavior.

## Scope
- Handle questions about theoretical background and algorithmic methods.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/details/doxygen_sphinx_ref.md`
- `docs/equations.rst`

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
- `src/equation_of_state/MOM_EOS.F90`
- `src/equation_of_state/MOM_EOS_base_type.F90`
- `src/equation_of_state/MOM_EOS_TEOS10.F90`
- `src/equation_of_state/MOM_EOS_Wright_full.F90`
- `src/equation_of_state/MOM_EOS_Roquet_SpV.F90`
- `src/equation_of_state/MOM_TFreeze.F90`
- `src/core/MOM_PressureForce.F90`
- `config_src/drivers/unit_tests/test_MOM_EOS.F90`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" config_src pkg src`).
