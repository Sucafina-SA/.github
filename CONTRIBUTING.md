# Contributing

Every research repository in this org follows one written standard:
**`docs/REPO_BUILD_GUIDE.md`**, vendored into each repo so you (or an agent) can
read it locally. The canonical copy lives in `Sucafina-SA/research-standards`.

## The short version

```powershell
uv sync --all-groups
uv run pre-commit install
uv run python scripts/check.py     # THE gate. Green means green.
```

- **`uv` only.** No pip, no venv, no poetry, no conda. Mixing them is how
  lockfiles drift, and a drifted lockfile means "works on my machine" stops
  being evidence of anything.
- **Everything runs through `uv run`.** Bare `python` uses the system
  interpreter and produces a confusing `ModuleNotFoundError`.
- **`src/` is imported and tested, never run. `scripts/` is run, never
  imported.** Shared logic between two scripts belongs in `src/`.
- **Branch, PR, review.** Direct pushes to `main` are blocked by an org
  ruleset on repos tagged `repo_class = trading-model`.
- **Never commit** `.env`, credentials, `*.duckdb`, `*.parquet`, `*.csv`. All
  are gitignored; do not `git add -f` around it. Put evidence in a markdown
  table or a JSON file.

## Starting a new repo

Use `Sucafina-SA/research-repo-template` — **Use this template**, then
`uv run python bootstrap.py --name my-repo`. Follow `NEW_REPO_CHECKLIST.md`.

Do not scaffold by hand. It is not faster and the result drifts from every other
repo immediately.

## If you are an agent

Read `AGENTS.md` at the repo root first, then the vendored build guide. Report
the truth about the gate: a false green removes the human's ability to trust any
other report you make.
