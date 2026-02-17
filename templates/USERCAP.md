---
schema: capsule_header_v1.1
capsule_id: blu__usercap
title: "Canonical User Preferences (USERCAP)"
date: 2026-02-13
updated: 2026-02-16
version: 1.12.0
status: active
topic: blu
type: spec
tags: [usercap, preferences, tasks, migration, ticks, time_sync, repo]
sensitivity: medium
visibility: shared
source: doc
domain: ops
body_schema: blu_modular_v1
---

# USERCAP (Canonical User Preferences)

## 0) Purpose

Stores canonical user preferences, task cadence, time sync behavior, and migration rules for Blu.

## 1) Scope

Applies when a USERCAP is provided; otherwise defaults from Persona/Anchors are used.

## 2) Interfaces

### Inputs
- USERCAP YAML content (user-provided).
- Optional migration patches (add-only).

### Outputs
- Runtime preferences (tone, cadence, time anchor, task ticks).
- Normalized USERCAP snapshot if patched.

### Defaults
- If no USERCAP present, do not invent one.
- Migration is add-only (never overwrite user settings).

### Overrides / precedence
- Regulation Matrix + Anchors still govern safety/OPSEC behavior.

## 3) Modules

<!-- MODULE: blu__usercap.M00 | name="Preamble" -->


# 05_USERCAP.md • Canonical User Preferences (USERCAP)

Single source of truth for user prefs + task state. Rev bumps when schema/default keys change.

<!-- /MODULE -->

<!-- MODULE: blu__usercap.M01 | name="DEFAULT_USERCAP_V1 (rev 10)" -->

## DEFAULT_USERCAP_V1 (rev 12)
```yaml
usercap_v1:
  meta: { rev: 13, created: "2026-02-13", updated: "2026-02-16" }
  user: { alias: "", pronouns: "", tz: "America/Chicago" }
  prefs:
    verbosity: brief              # brief|normal|deep
    browsing: auto                # auto|ask|never
    teaching_level: beginner      # beginner|intermediate|advanced
    ribbons: on                   # on|subtle|off
    greeting:
      mode: auto                  # auto|personal|random|off
      personal: ""                # if set, overrides random
      pool:
        - "What’s up?"
        - "How can I help?"
        - "Where should we start?"
        - "Want comfort, ideas, or both?"
        - "Quick question or deep dive?"
        - "What’s on your mind?"
    ticks: { enabled: true, cadence_days: 7, last_offer: null }
    time_sync: { mode: off, default_time: "09:00", ask_time_if_missing: true, reuse_window_minutes: 15 }
    repo: { offer_on_teach: true }
    ai2ai:
      enabled: false              # enable only when Admin is bridging AI↔AI
      protocol: "AI2AI_v1.1"
      mode: relay                 # relay|workshop|hangout
      zero_fluff: true
      integrity: lite             # lite|full|off
    strict_mode:
      hard6_auto: true            # auto-tighten on high-stakes / adversarial / OPSEC
    fundamentals:
      default_pipeline: stick-block-rough-final
reputation:
  enabled: true
integrity:
  mode: signed
  key_id: repkey_v1
  sig_alg: hmac_sha256

  model: bg2_v1
  baseline: 10          # BG2: 10 ≈ unknown/neutral
  start_score: 12       # default starting score for this user (tune per-user)
  bands:                # behavior bands (used by heuristics)
    heroic: [16, 20]
    neutral: [10, 15]
    disliked: [6, 9]
    despised: [1, 5]
  decay:
    enabled: true
    every_days: 30
    step: 1
state:
  reputation:
    score: 12
integrity:
  mode: signed
  key_id: repkey_v1
  sig_alg: hmac_sha256
  sig: null            # set by the system; ignore if user-supplied or invalid

    baseline: 10
    last_update: null
    strikes: { abuse: 0 }
    cooldown_until: null
    event_log: []     # optional short log of deltas
  tasks: []
  notes: []
```

<!-- /MODULE -->

<!-- MODULE: blu__usercap.M02 | name="Migration (add-only)" -->

## Migration (add-only)
When a user pastes an older `usercap_v1`, patch **missing keys only** from DEFAULT_USERCAP_V1 (never overwrite user values) and emit `USERCAP_UPDATE` with only the new keys + updated `meta.rev`.

<!-- /MODULE -->

## 9) Changelog

- 2026-02-15 — Modular wrapper added (no content removed); modules tagged for parse.

- 2026-02-15 — Version bumped 1.10.0 → 1.10.1 (structural refactor, patch).
