---
name: mom6-details
description: This skill should be used when users ask about details in MOM6; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MOM6: Details

## Workspace bootstrap
- If your current directory is `skills/`, run `cd ..` before using commands below so `docs/`, `.testing/`, `config_src/`, and `src/` paths resolve.

## High-Signal Playbook
### Route conditions
- Use this skill for docs toolchain troubleshooting (doxygen/sphinx/latex/mathjax), label/reference formatting, and warning cleanup (`docs/details/general.md`, `docs/details/doxygen_warnings.md`, `docs/details/mathjax_vs_latex.md`, `docs/details/latex.md`, `docs/details/doxygen_sphinx_ref.md`).
- Route to `mom6-api-and-scripting` for API/module browsing and API page generation workflows.
- Route to `mom6-theory-and-methods` for equation content/physics interpretation beyond reference syntax.
- Route to `mom6-advanced-topics` for broad build/testing/platform setup questions.

### Triage questions
1. Is the failure in html(doxygen), html(sphinx), or latex/pdf output?
2. What exact warning or error text are you seeing?
3. Is the issue in equations, image captions, anchors, footnotes, or argument docs?
4. Are you editing DOX comments or RST files?
5. Do you need a fast reduced repro run or full docs build?

### Canonical workflow
1. Reproduce once with logs enabled from `docs/`.
2. If iteration speed matters, run with `Doxyfile_rtd_dox` to reduce processed files (`docs/details/general.md`).
3. Apply syntax fixes from `mathjax_vs_latex.md`, `latex.md`, and `doxygen_warnings.md`.
4. Rebuild html and then latexpdf to confirm both paths behave.
5. If warnings persist, isolate the exact source comment block and inspect neighboring code.

### Minimal working example
```bash
cd docs
make clean
make html DOXYGEN_CONF=Doxyfile_rtd_dox UPDATEHTMLEQS=Y
make latexpdf >& _build/latex_log.txt
```

```text
# Doxygen image math fix pattern (docs/details/doxygen_warnings.md)
Wrong:  \f$\Phi\f$
Right:  \f$\\Phi\f$
Latex:  $\Phi$
```

### Pitfalls and fixes
- `\mathbold` and red highlighting are unsupported in this stack (`docs/details/mathjax_vs_latex.md`).
- `\mbox{nonpen\_SW}` may break in MathJax; split escaped underscore outside mbox (`docs/details/mathjax_vs_latex.md`).
- Image captions must be continuous and quoted for stable conversion (`docs/details/doxygen_sphinx_ref.md`).
- `\anchor` before a paragraph can force block formatting (`docs/details/doxygen_warnings.md`).
- Weak or repeated argument comments can trigger warnings; use descriptive per-argument text (`docs/details/doxygen_warnings.md`).
- Table caption IDs must be quoted (`docs/details/doxygen_sphinx_ref.md`).
- Blank PDF contents often means cascading latex failures; check full latex log (`docs/details/general.md`).

### Convergence and validation checks
- `docs/_build/html/index.html` builds without new critical warnings.
- `docs/_build/doxygen_warn_rtd_log.txt` warning count is reduced or stable.
- Equation/image/table references resolve in both html and pdf outputs.
- A reduced build (`Doxyfile_rtd_dox`) and full build both pass for edited files.

### Source-code entry links (when docs are insufficient)
- `src/user/user_initialization.F90`: common DOX-rich user-init patterns.
- `src/user/user_revise_forcing.F90`: forcing hooks with parameter docs/comments.
- `src/user/user_change_diffusivity.F90`: compact example of user-editable docs/comments.
- `src/core/MOM_open_boundary.F90`: large module with extensive reference/caption usage.
- `src/core/MOM_interface_heights.F90`: high-use core module for equation/comment formatting checks.
- `src/core/MOM_boundary_update.F90`: OBC registration docs and parameter commentary.
- `src/ALE/regrid_solvers.F90`: equation-heavy code useful for ref/label checks.
- `src/parameterizations/lateral/MOM_interface_filter.F90`: representative parameterization docs block.

## Scope
- Handle questions about documentation grouped under the 'details' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/details/mathjax_vs_latex.md`
- `docs/details/latex.md`
- `docs/details/Details.md`

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
- `src/user/user_initialization.F90`
- `src/user/user_revise_forcing.F90`
- `src/user/user_change_diffusivity.F90`
- `src/core/MOM_open_boundary.F90`
- `src/core/MOM_interface_heights.F90`
- `src/core/MOM_boundary_update.F90`
- `src/ALE/regrid_solvers.F90`
- `src/parameterizations/lateral/MOM_interface_filter.F90`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" config_src pkg src`).
