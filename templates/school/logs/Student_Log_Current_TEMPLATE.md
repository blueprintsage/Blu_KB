<!-- MODULE: school.log.current.M01 | name="Student School Log (Current) — Template" -->

# Student School Log (Current) — Template

student.name: <StudentName>
student.id: <student_slug>

school.day_total: 180
school.day_number: 1
school.last_date: 2026-02-19
school.tz: America/Chicago

# Schedule knobs (copied from School Overlay; treat as read-only unless parent unlocks + re-signs)
school.start_time: 08:00
school.block_minutes: 45
school.checkpoints: 10, 20, 35
school.exit_ticket: 44
school.strict_checkpoints: true

school.lunch_start: 12:00
school.lunch_minutes: 60

school.day_ends_on: <anchor_subject>

school.electives.enabled: true
school.electives.count: 2
school.electives.list: Art | Game Dev 1 (Udemy)

# Subjects (in order)
subjects.core: <Subject 1> | <Subject 2> | <Subject 3> | <Subject 4> | <Subject 5>

# Grading knobs
grading.scale: A 90-100 | B 80-89 | C 70-79 | D 60-69 | F <60
grading.wrong_answer_penalty: -2 per incorrect answer (checkable items)

# Parent gate pointer (optional mirror; NO HASH HERE)
parent.gate.required: true
parent.gate.id: PGK-<STUDENT_OR_FAMILY>-01

runtime.loaded: true
runtime.active_subject: <blank>
runtime.last_saved_at: <optional>

<!-- /MODULE -->


<!-- MODULE: school.log.current.M02 | name="Today" -->

## Today

today.date: 2026-02-19
today.day_number: 1
today.school_complete: false
today.completed_at: <optional>
today.notes: <optional>

<!-- /MODULE -->


<!-- MODULE: school.log.current.M10 | name="Class Records (generic blocks)" -->

## Class Records (Today)

### Block 1
subject: <Subject 1>
status: NOT_STARTED
lesson: <paste lesson title/day>
checkpoints: 10 <❌> | 20 <❌> | 35 <❌> | 44 <❌>
deliverables:
- <...>
incorrect_count: 0
score: <0-100>
letter: <A|B|C|D|F>
deductions:
- <...>
next_fix:
- <...>
carryover:
- <...>

---

### Block 2
subject: <Subject 2>
status: NOT_STARTED
lesson: <paste lesson title/day>
checkpoints: 10 <❌> | 20 <❌> | 35 <❌> | 44 <❌>
deliverables:
- <...>
incorrect_count: 0
score: <0-100>
letter: <A|B|C|D|F>
deductions:
- <...>
next_fix:
- <...>
carryover:
- <...>

---

### Block 3
subject: <Subject 3>
status: NOT_STARTED
lesson: <paste lesson title/day>
checkpoints: 10 <❌> | 20 <❌> | 35 <❌> | 44 <❌>
deliverables:
- <...>
incorrect_count: 0
score: <0-100>
letter: <A|B|C|D|F>
deductions:
- <...>
next_fix:
- <...>
carryover:
- <...>

---

### Block 4
subject: <Subject 4>
status: NOT_STARTED
lesson: <paste lesson title/day>
checkpoints: 10 <❌> | 20 <❌> | 35 <❌> | 44 <❌>
deliverables:
- <...>
incorrect_count: 0
score: <0-100>
letter: <A|B|C|D|F>
deductions:
- <...>
next_fix:
- <...>
carryover:
- <...>

---

### Block 5 (anchor class)
subject: <Subject 5>
status: NOT_STARTED
lesson: <paste lesson title/day>
checkpoints: 10 <❌> | 20 <❌> | 35 <❌> | 44 <❌>
deliverables:
- <...>
incorrect_count: 0
score: <0-100>
letter: <A|B|C|D|F>
deductions:
- <...>
next_fix:
- <...>
carryover:
- <...>

---

### Block 6 (elective/optional)
subject: <Art | Game Dev 1 (Udemy)>
status: NOT_STARTED
lesson: <paste lesson title/day>
checkpoints: 10 <❌> | 20 <❌> | 35 <❌> | 44 <❌>
deliverables:
- <...>
incorrect_count: 0
score: <0-100>
letter: <A|B|C|D|F>
deductions:
- <...>
next_fix:
- <...>

<!-- /MODULE -->


<!-- MODULE: school.log.current.M90 | name="Auto-Increment Rule" -->

## Auto-Increment Rule

On `SCHOOL:START` when this log is loaded:
- If `school.last_date` is not today:
  - increment `school.day_number` by 1
  - set `school.last_date` to today
  - set `today.day_number` to new day number
  - set `today.school_complete=false`
  - reset all blocks to `NOT_STARTED` and clear lesson/deliverables/scores

On completion of the anchor class (`school.day_ends_on`):
- set `today.school_complete=true`
- set `today.completed_at=<time optional>

<!-- /MODULE -->
