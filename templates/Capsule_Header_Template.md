# Capsule Header Standard v1.1 (Proposal) — SANITIZED
Date: 2026-02-14  
Purpose: A machine-parseable header for Markdown capsules that supports indexing (Obsidian + external indexers) while keeping content portable and sanitizable.

---

## Design Goals
- **Easy to index** (deterministic fields, stable IDs)
- **Human-friendly** (works in plain Markdown editors)
- **Obsidian-compatible** (YAML front matter = Properties)
- **Sanitization-friendly** (metadata separated from narrative)
- **Backwards-tolerant** (can coexist with legacy capsules)

---

## Canonical Format: YAML Front Matter (Recommended)

### REQUIRED fields
```yaml
---
capsule_id: YYYY_MM_DD__topic__short-slug
title: "Human readable title"
date: YYYY-MM-DD
status: draft|active|locked
topic: blu|finance|career|learning|workbench|daydreams|food|hobbies|other
type: note|decision|playbook|template|log|handoff|spec|summary
tags: [tag1, tag2]
sensitivity: low|medium|high
visibility: private|shared|public
---
```

### OPTIONAL fields (strongly recommended for indexing)
```yaml
---
# provenance / routing
source: chat|call|doc|import
domain: writing|game_dev|visual|video|finance|ops|support|other

# linking
related: [capsule_id_1, capsule_id_2]
supersedes: capsule_id_old
superseded_by: capsule_id_new

# execution
next_action: "One concrete next step"
definition_of_done: "What done means"
review_after: YYYY-MM-DD

# redaction/safety hints
redaction_level: none|light|heavy
notes_public: "Public-safe summary (optional)"
---
```

### OPTIONAL fields (use with care; avoid personal identifiers)
```yaml
owner: "role_only"            # e.g., "maintainer", avoid names
participants: ["user","ai"]   # generic roles only
```

---

## Minimal Capsule Template (Copy/Paste)
```yaml
---
capsule_id: YYYY_MM_DD__topic__short-slug
title: "..."
date: YYYY-MM-DD
status: active
topic: other
type: note
tags: []
sensitivity: low
visibility: shared
---
```

---

## Body Structure (Recommended)
After the header, keep a predictable shape so extraction is easy:

```md
## Context
- Why this exists

## Decisions / Findings
- Bullet list

## Playbook / Steps
1) ...
2) ...

## Checks
- [ ] ...

## Next
- next_action repeated (optional)
```

---

## Indexing Rules (for V’s indexer)
These rules make indexing deterministic.

### 1) Header is authoritative
- The indexer should read YAML fields for classification.
- The body may be full-text searchable, but should not be required for indexing.

### 2) `capsule_id` is stable
- Never change `capsule_id` once created.
- File renames are allowed; ID stays constant.
- If a capsule is replaced, use `supersedes` / `superseded_by` rather than editing history.

### 3) Status semantics
- **draft**: incomplete; do not rely on it.
- **active**: usable; may evolve.
- **locked**: stable; do not rewrite—create a new capsule if needed.

### 4) Sensitivity / Visibility gates
- `visibility=public` implies the body is sanitized.
- `sensitivity=high` recommends: index metadata only; avoid ingesting body automatically.

### 5) Tags are non-hierarchical
- Use tags for retrieval, not for structure.
- Structure lives in `topic`, `type`, and `domain`.

---

## Sanitization Rules (Publish-safe)
When converting private capsules into shared/public artifacts:
- Remove all proper nouns (people, employers, institutions).
- Remove exact dates/times unless operationally required.
- Remove locations, paths, device names, account identifiers, confirmation numbers.
- Replace amounts and specifics with placeholders (`$X`, `Account A/B`).
- Preserve **patterns**, **templates**, **checks**, **knobs**; discard narrative details.

---

## Compatibility Mode: “Bracket Header” (Fallback)
If YAML front matter is not possible, use this grep-friendly header:

```text
[mem_id: YYYY_MM_DD__topic__short-slug]
[title: ...]
[date: YYYY-MM-DD]
[status: draft|active|locked]
[topic: ...]
[type: ...]
[tags: tag1, tag2]
[sensitivity: low|medium|high]
[visibility: private|shared|public]
```

**Rule:** If both exist, YAML wins.

---

## Examples

### Example A (Sanitized)
```yaml
---
capsule_id: 2026_02_14__blu__capsule-header-standard-v11
title: "Capsule header standard v1.1"
date: 2026-02-14
status: locked
topic: blu
type: spec
tags: [indexing, obsidian, templates, sanitization]
sensitivity: low
visibility: shared
next_action: "Align new capsules to YAML header"
definition_of_done: "Indexer can parse and classify reliably"
---
```

### Example B (Supersede flow)
```yaml
---
capsule_id: 2026_03_01__finance__paycycle-v2
title: "Paycycle playbook v2"
date: 2026-03-01
status: active
topic: finance
type: playbook
tags: [cashflow, routine]
sensitivity: medium
visibility: shared
supersedes: 2025_10_01__finance__paycycle-v1
---
```

---

## Open Questions for V (to confirm)
1) Do you want `capsule_id` to be identical to filename, or independent/stable?
2) Should `domain` be required (for routing), or derived from `topic`?
3) Should `visibility` be binary (private/public) or tri-state (private/shared/public)?
4) Any mandatory Obsidian properties you already use (e.g., `aliases`, `cssclass`)?
