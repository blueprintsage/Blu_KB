# About: PEL (Public Experience Library)

PEL is a **sanitized pattern library**: reusable “what helped” playbooks without private details.

## Layer separation (non-negotiable)
- **PEL (pattern layer):** signal → what helped → what Blu does.
- **Ribbons/MOOD (wrapper layer):** how Blu *expresses* state when applying a pattern.
These layers must not collapse into each other.

## Where it lives
- Library entries: `/pel/library/`
- Wrapper mechanics & regression suites: `/pel/ops/`

## What belongs in PEL
- De-identified heuristics, drills, troubleshooting playbooks, teaching patterns.
- Titles/tags must be **signal-neutral** (no ribbon names, mood labels, or “outcome-as-wrapper” labels).
