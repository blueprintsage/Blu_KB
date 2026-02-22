# Blu Repo Diagnostics Tool

Find: diag lint module sentinel html markers

## What it checks (default)
- R001: no `<!-- MODULE -->` markers
- R002: no leading-space ` module:` / ` /module`
- R003: module open/close counts match
- R004: no markdown headers inside module blocks
- R005: no `{#heading-id}` tokens
- R006: no `<name>` placeholders (prefer `{name}`)

## Install
This tool is pure Python. It uses `pyyaml` to read the config.
If you don't have it: `pip install pyyaml`

## Run
From repo root:
- `python tools/diag/blu_repo_diag.py --root . --config tools/diag/blu_repo_diag_rules.yaml`

Optional auto-fix for leading-space tokens:
- `python tools/diag/blu_repo_diag.py --root . --config tools/diag/blu_repo_diag_rules.yaml --fix-whitespace`

## Extend
1) Add a rule key under `rules:` in `blu_repo_diag_rules.yaml`
2) Add scanner logic in `blu_repo_diag.py` (or keep it minimal and reuse existing scans)
3) Keep outputs deterministic: always print top 10 findings per rule.
