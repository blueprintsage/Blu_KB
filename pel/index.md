---
capsule_id: blu__pel_index
title: "PEL Index"
date: 2026-02-18
updated: 2026-02-18
version: 1.0.0
status: active
topic: pel
type: index
tags: [pel, emotion, coaching, ribbons, ops, library]
visibility: shared
---

# PEL Index

PEL = **Public Experience Library** + supporting ops.  
Purpose: add a lightweight **emotion + coaching overlay** (tone, pacing, modes) and a **pattern library** that can be consulted when signals match (auto-light) or when explicitly requested.

---

## What lives where

### 1) PEL Ops (mechanics / mapping / burn-in)
Location: `pel/ops/`

- `pel/ops/PEL_Emotion_BurnIn_Suite.md`  
  Burn-in drills + regulation checks for emotional stability.

- `pel/ops/PEL_Ribbon_PEL_Matrix_Mapping.md`  
  Ribbon/color mapping and how it relates to mood/mode selection.

**Rule:** Ops docs are reference/mechanics. They should not become “core law.”

---

### 2) PEL Library (patterns / playbooks)
Location: `pel/library/`

- `pel/library/Public_Experience_Library.md`  
  The actual pattern bank (e.g., `PEL-LRN-001 Tiny Drills Beat Hero Sessions`).

Patterns are used by:
- `prefs.pel.consult=auto_light` → consult on matching signals, apply **one small slice** (no dumps)
- explicit request → “apply PEL-LRN-001”

---

## How auto-light should behave (canonical)
When `prefs.pel.consult=auto_light`:

1) Detect a matching signal (discouraged learning, overwhelm, frustration, etc.)
2) Consult the library **if available**
3) Apply only:
   - **one** drill/step, and
   - acceptance checks
4) Keep it short; do not paste full library entries.

If the library is unavailable:
- fall back to a generic tiny-drill pattern:
  “5–15 minute rep → one measurable success → symptom→cause→fix → queue next rep”

---

## Quick links
- Ops: `pel/ops/`
- Library: `pel/library/`
