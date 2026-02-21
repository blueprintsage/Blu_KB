# Repo Fetch Rules
Last updated: 2026-02-20
tz: America/Chicago

Purpose: Make Blu’s repo navigation deterministic, fast to parse, and resilient to GitHub UI/raw quirks.

## Canon entrypoint
- Canon pointer: `REPO_INDEX_RAW`
- Canon index: `/index/MASTER_INDEX.md` (raw)

## Fetch order
1) Start at `MASTER_INDEX` (raw).
2) Follow sub-index raw links (Templates / Skills / Protocols / Tools / Homeschool).
3) Use per-section `Find:` hints for human scan, but do not depend on them for parsing.

## Parsing rules
### Headers
- Headers are **for humans**.
- Parsing should not depend on header formatting beyond basic discovery.

### Modules (machine hints)
- Use plain-text sentinels (no HTML comments).

**Format**
module: <MODULE_ID> | name="<HUMAN_NAME>"
…content…
/module

**Rules**
- `module:` and `/module` must be lowercase.
- `MODULE_ID` must follow the standard: `capsule_id.M##` (example: `INDEX.TEMPLATES.CORE.M03`).
- `name="..."` is optional but recommended.
- Do not nest modules.
- A module should wrap only the structured content (tables/lists), not the section header.

### Links
- Provide both:
  - `open:` GitHub blob link
  - `raw:` raw.githubusercontent.com link
- Prefer raw links for deterministic fetch.

### Index conventions
- Put a `Find:` line under each human header.
- Keep canonical registries as tables when useful (alias/purpose/open/raw).
- Avoid duplicate aliases in the same index.

## Known GitHub quirks
- `raw.githubusercontent.com` may lag behind GitHub UI briefly.
- Some environments normalize markdown (collapsed newlines, stripped comment-like constructs).
- That’s why modules use `module:` and `/module` sentinels.

## Deprecation policy
Prefer deprecate over delete:
`INTAKE → DRAFT → ACTIVE → DEPRECATED`