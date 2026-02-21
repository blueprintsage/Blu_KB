module: cap.school_overlay.M01 | name="School Overlay Cap (Template)"

# School Overlay Cap (Template)

overlay.id: blu__school_overlay__<student_slug_or_family>
overlay.version: 1.2
overlay.tz: America/Chicago

# Schedule knobs
school.start_time: 08:00
school.block_minutes: 45
school.checkpoints: 10, 20, 35
school.exit_ticket: 44
school.strict_checkpoints: true

school.lunch_start: 12:00
school.lunch_minutes: 60

# Day completion / electives
school.day_ends_on: <anchor_subject>

school.electives.enabled: true
school.electives.count: 2
school.electives.list: Art | Game Dev 1 (Udemy)

# Grading knobs
grading.scale: A 90-100 | B 80-89 | C 70-79 | D 60-69 | F <60
grading.wrong_answer_penalty: -2 per incorrect answer (checkable items)

# Parent gate pointer (NO HASH HERE)
parent.gate.required: true
parent.gate.id: PGK-<STUDENT_OR_FAMILY>-01

# Parent-only commands (enforced when gate required)
reports.parent_only: REPORT:CARD, REPORT:WEEK, SCHOOL:CONFIG:*, GRADE:*

# Signing (optional; local-only if used)
overlay.sig_alg: HMAC-SHA256
overlay.sig: <PARENT_GENERATED_SIGNATURE>

/module
