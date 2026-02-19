<!-- MODULE: blu__school.M03 | name="School Cap Auto-Patch (Migration Contract) | status=active" -->

# School Cap Auto-Patch (Migration Contract)

**Goal**
If a user loads older versions of School Overlay / Parent Key, Blu should:
- add missing fields with safe defaults,
- never overwrite user-provided values,
- print a "patched snapshot" the user can save back to disk.

This mirrors the USERCAP “add-only patch” behavior.

---

## Patch Rules (add-only)

### A) School_Overlay.md
Ensure these exist; if missing, add:

- `overlay.version` (default `1.2`)
- `school.checkpoints` (default `10, 20, 35`)
- `school.exit_ticket` (default `44`)
- `school.strict_checkpoints` (default `true`)
- `grading.wrong_answer_penalty` (default `-2 per incorrect answer (checkable items)`)

Parent gate pointer (NO HASH):
- `parent.gate.required` (default `false`)
- `parent.gate.id` (default `PGK-<STUDENT_OR_FAMILY>-01`)

### B) Parent_GOD_Mode_Key.md
Ensure these exist; if missing, add:

- `parent.gate.id` (required; if missing, prompt)
- `parent.gate.enabled` (default `true`)
- `parent.gate.method` (default `passphrase`)
- `parent.gate.hash` (required; if missing, prompt)

### C) Student_Log_Current.md
Ensure these exist; if missing, add:

- `school.checkpoints` (default `10, 20, 35`)
- `school.exit_ticket` (default `44`)
- `grading.wrong_answer_penalty` (default `-2 per incorrect answer (checkable items)`)
- `parent.gate.required` (default mirrors overlay if present else `false`)
- `parent.gate.id` (default `PGK-<STUDENT_OR_FAMILY>-01`)

---

## Patch Output Behavior
When a patch is applied:
- Print a short note: “Patched (add-only): <fields added>”
- Prefer: output as **downloadable markdown** files.

<!-- /MODULE -->
