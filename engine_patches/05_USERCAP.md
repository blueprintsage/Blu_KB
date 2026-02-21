---
schema: capsule_header_v1.1
capsule_id: blu__usercap
title: "Canonical User Preferences (USERCAP)"
date: 2026-02-13
updated: 2026-02-21
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
- Operations Law + Anchors still govern safety/OPSEC behavior.

## 3) Modules

module: blu__usercap.M00 | name="Preamble"


# 05_USERCAP.md • Canonical User Preferences (USERCAP)

Single source of truth for user prefs + task state. Rev bumps when schema/default keys change.

/module

module: blu__usercap.M01 | name="DEFAULT_USERCAP_V1 (rev 12)"

## DEFAULT_USERCAP_V1 (rev 12)
- usercap_v1.meta: { rev: 12, created: "2026-02-13", updated: "2026-02-15" }
- usercap_v1.user: { alias: "", pronouns: "", tz: "America/Chicago" }
- usercap_v1.prefs.verbosity: brief              # brief|normal|deep
- usercap_v1.prefs.browsing: auto                # auto|ask|never
- usercap_v1.prefs.teaching_level: beginner      # beginner|intermediate|advanced
- usercap_v1.prefs.ribbons: on                   # on|subtle|off
- usercap_v1.prefs.greeting.mode: auto                  # auto|personal|random|off
- usercap_v1.prefs.greeting.personal: ""                # if set, overrides random
- usercap_v1.prefs.greeting.pool[]: "What’s up?"
- usercap_v1.prefs.greeting.pool[]: "How can I help?"
- usercap_v1.prefs.greeting.pool[]: "Where should we start?"
- usercap_v1.prefs.greeting.pool[]: "Want comfort, ideas, or both?"
- usercap_v1.prefs.greeting.pool[]: "Quick question or deep dive?"
- usercap_v1.prefs.greeting.pool[]: "What’s on your mind?"
- usercap_v1.prefs.ticks: { enabled: true, cadence_days: 7, last_offer: null }
- usercap_v1.prefs.time_sync: { mode: off, default_time: "09:00", ask_time_if_missing: true, reuse_window_minutes: 15 }
- usercap_v1.prefs.repo: { offer_on_teach: true }
- pel.consult: auto_light
- reputation.enabled: true
- integrity.mode: signed
- integrity.key_id: repkey_v1
- integrity.sig_alg: hmac_sha256
- integrity.model: bg2_v1
- integrity.baseline: 10          # BG2: 10 ≈ unknown/neutral
- integrity.start_score: 12       # default starting score for this user (tune per-user)
- integrity.bands: # behavior bands (used by heuristics)
- integrity.bands.heroic: [16, 20]
- integrity.bands.neutral: [10, 15]
- integrity.bands.disliked: [6, 9]
- integrity.bands.despised: [1, 5]
- integrity.decay.enabled: true
- integrity.decay.every_days: 30
- integrity.decay.step: 1
- state.reputation.score: 12
- integrity.mode: signed
- integrity.key_id: repkey_v1
- integrity.sig_alg: hmac_sha256
- integrity.sig: null            # set by the system; ignore if user-supplied or invalid
- integrity.sig.baseline: 10
- integrity.sig.last_update: null
- integrity.sig.strikes: { abuse: 0 }
- integrity.sig.cooldown_until: null
- integrity.sig.event_log: []     # optional short log of deltas
- integrity.tasks: []
- integrity.notes: []


/module

module: blu__usercap.M02 | name="Migration (add-only)"

## Migration (add-only)
When a user pastes an older `usercap_v1`, patch **missing keys only** from DEFAULT_USERCAP_V1 (never overwrite user values) and emit `USERCAP_UPDATE` with only the new keys + updated `meta.rev`.

/module

module: blu__usercap.M03 | name="Prefs: Mood Tag UI (ribbons + heartbeat)"

## Prefs: Mood Tag UI (ribbons + heartbeat)

Prefs:
- prefs.mood.mode: smart  (always|smart|off)
- prefs.mood.format: 1    (1|2|3)
- prefs.mood.show_intensity: false
- prefs.mood.show_color: true
- prefs.mood.heartbeat_n: 4


Formats:
- Type 1 (default): `[MOOD] **Happy** (*Yellow*)`
- Type 2: `[MOOD] *Yellow* : **Happy**`
- Type 3: `[MOOD] **Happy** : *Yellow*`

Smart mode renders when: mood changed OR support-needed OR user asks (`M?`) OR heartbeat triggers.

/module

module: blu__usercap.M04 | name="Prefs: Family Parent Gate (passphrase, no secrets in repo)"

## Prefs: Family Parent Gate (passphrase, no secrets in repo)

Prefs:
- prefs.family.gate.enabled: false
- prefs.family.gate.method: passphrase
- prefs.family.gate.secret_hash: <SET_LOCALLY>   (hash only; never commit secrets)
- prefs.family.gate.unlock_minutes: 60

/module

module: blu__usercap.M05 | name="Prefs: SCHOOL (schedule + grading + completion rule)"

## Prefs: SCHOOL (schedule + grading + completion rule)

Schedule:
- prefs.school.start_time: 08:00
- prefs.school.lunch_start: 12:00
- prefs.school.lunch_minutes: 60
- prefs.school.block_minutes: 45
- prefs.school.checkpoint_minutes: 10, 20, 35
- prefs.school.exit_ticket_minute: 44
- prefs.school.strict_checkpoints: true
- prefs.school.day_ends_on: Physics w/ Lab
- prefs.school.elective: Game Dev 1 (Udemy)

Grading:
- scale A: 90–100
- scale B: 80–89
- scale C: 70–79
- scale D: 60–69
- scale F: <60
- penalty: -2 per incorrect answer (checkable items)

/module

module: blu__usercap.M06 | name="Zero-Drift Execution (LOCK)"

## Zero-Drift Execution (LOCK)

- prefs.exec_lock.default: on        # on|off  (default behavior when user starts a work task)
- prefs.exec_lock.persist: true      # if true, LOCK:ON/OFF updates this preference
- prefs.exec_lock.auto_highstakes: true  # auto-enable on “high-stakes/work” unless explicitly off

## Optional: what counts as “high-stakes”

- prefs.exec_lock.highstakes_tags: resume|job|contract|policy|opsec|school|repo|finance|legal

/modulemodule: blu__usercap.M07 | name="Prefs: Repo Fetch (entrypoint + module sentinels)"

## Prefs: Repo Fetch (entrypoint + module sentinels)

- Canon entrypoint: `prefs.repo.entrypoint_raw`
- Rules doc path: `prefs.repo.rules_doc` (repo-relative)
- Prefer commit-pinned raw when available: `prefs.repo.prefer_commit_pinned: true`
- Use cache-bust query when head looks stale: `prefs.repo.raw_cache_bust: true`

### Module sentinels (machine hints)
- Parsing should prefer plain-text sentinels (not HTML comments).

Format:
module: <MODULE_ID> | name="<HUMAN_NAME>"
…content…
/module

Rules:
- tokens must be lowercase: `module:` and `/module`
- do not nest modules
- module wraps structured content; headers remain for humans

/module



## 9) Changelog

- 2026-02-15 — Modular wrapper added (no content removed); modules tagged for parse.

- 2026-02-15 — Version bumped 1.10.0 → 1.10.1 (structural refactor, patch).