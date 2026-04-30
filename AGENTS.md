# AGENTS.md

## Repo shape
- This is a notebook + LaTeX report repo, not a package/workspace repo: no `package.json`, `pyproject.toml`, `requirements*.txt`, CI config, or test harness was found.
- Computational work lives in `scr/project.ipynb`; there are no importable Python modules or `src/` package.
- Report source lives in `doc/main.tex` and imports `doc/scr/preamble.tex`, `doc/scr/macros.tex`, and `doc/scr/letterfonts.tex`.

## Commands
- No scripted install/build/test/lint commands are declared in the repo.
- Observed report build flow is XeLaTeX -> xdvipdfmx from `doc/`:
  ```sh
  xelatex -output-directory=build main.tex
  xdvipdfmx -o build/main.pdf build/main.xdv
  ```
- The notebook uses Python with `numpy`, `matplotlib`, and `scipy`; notebook metadata records kernel display name `phys` and Python `3.10.19`.

## Notebook gotchas
- `scr/project.ipynb` is execution-order sensitive: `pbc_Hamiltonian` and `obc_Hamiltonian` are defined for the 1D tight-binding model, then redefined later for the SSH model.
- The notebook stores large `image/png` outputs inline, so small plot changes can create large diffs.
- For the PBC tight-binding dispersion, use an `E(k)` plot with `k = 2πm/N`; an eigenvalue-index plot is only a sorted spectrum comparison, not a dispersion relation.

## LaTeX/report gotchas
- `doc/main.tex` includes `doc/fig/Question 1/Eigenvalues_PBC_OBC.png`; quote paths in shell commands because `Question 1` contains a space.
- `.gitignore` only ignores `.DS_Store`; TeX build artifacts and notebook outputs are currently versioned/noisy.
- `doc/scr/build/template.*` appears to be stale build output: it references a `template.tex` source that is not present.
