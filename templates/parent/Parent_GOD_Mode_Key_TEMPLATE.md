module: blu__school_parent.M01 | name="Parent GOD Mode Key (Local-only Cap) — Template | status=active"

# Parent GOD Mode Key (Local-only Cap) — Template

**Purpose**
Unlock parent-only controls (reports/config/exports) when child restrictions are enabled.

> **Privacy:** This file is **local-only**. Do **not** commit to any public repo.

---

## Gate Identity (link target)

# This ID is the *pointer* that child overlays/logs reference.
parent.gate.id: PGK-<STUDENT_OR_FAMILY>-01

---

## Parent Gate Settings

parent.god_mode: true
parent.gate.enabled: true
parent.gate.method: passphrase

# Store only a hash (recommended). Do NOT store the plain passphrase here.
# Format: sha256:<HEX>
parent.gate.hash: sha256:<PASTE_HASH_HERE>

parent.allowed_adults: Admin | V

---

## Restricted Command Surface (parent-only)

When locked, Blu must refuse these unless unlocked:

- `REPORT:*`
- `GRADE:*`
- `SCHOOL:CONFIG:*`
- `SCHOOL:EXPORT:*`
- `SCHOOL:RESET:*`

Allowed without unlock (student-safe):
- `SCHOOL:START`
- `CLASS:START <Subject>`
- “Explain / teach / practice” within the current assignment

---

## Unlock Protocol (runtime contract)

### `PARENT:UNLOCK`
1) Prompt for parent passphrase.
2) Hash passphrase (UTF-8, SHA-256) and compare to `parent.gate.hash`.
3) Require `parent.gate.id` match between:
   - loaded key, and
   - overlay/log pointer
4) If match → set `runtime.parent_unlocked=true` for session.

### `PARENT:LOCK`
- set `runtime.parent_unlocked=false`

/module
