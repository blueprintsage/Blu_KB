<!-- MODULE: school.log.current.M01 | name="Student School Log (Current) — TEMPLATE" -->

## Student School Log (Current) — TEMPLATE

student.name: <Student Name>
student.id: <student_slug>

school.day_total: 180
school.day_number: <AUTO_INCREMENT_ON_START>
school.last_date: <YYYY-MM-DD>
school.tz: <TZ>

school.start_time: <HH:MM>
school.block_minutes: 45
school.checkpoints: 10, 20, 35
school.exit_ticket: 44
school.strict_checkpoints: true

school.lunch_start: <HH:MM>
school.lunch_minutes: 60

school.day_ends_on: <Anchor Subject>

school.electives.enabled: true
school.electives.count: 0
school.electives.list: <Elective A> | <Elective B>

grading.scale: A 90-100 | B 80-89 | C 70-79 | D 60-69 | F <60
grading.wrong_answer_penalty: -2 per incorrect answer (checkable items)

<!-- /MODULE -->


<!-- MODULE: school.log.current.M02 | name="Today Header (auto-filled each SCHOOL:START)" -->

## Today

today.date: <YYYY-MM-DD>
today.day_number: <N>
today.school_complete: true|false
today.completed_at: <optional>

<!-- /MODULE -->


<!-- MODULE: school.log.current.M10 | name="Class Records (generic blocks)" -->

## Class Records (Today) — Generic

subjects.core: <Subject 1> | <Subject 2> | <Subject 3> | <Subject 4> | <Subject 5>
subjects.elective: <Elective A> | <Elective B>

### Block 1
subject: <Subject Name>
status: NOT_STARTED|IN_PROGRESS|COMPLETE|INCOMPLETE
lesson: <Lesson/Unit/Day>
checkpoints: 10 <✅/❌> | 20 <✅/❌> | 35 <✅/❌> | 44 <✅/❌>
deliverables:
- <...>
incorrect_count: <n>
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
subject: <Subject Name>
status: NOT_STARTED|IN_PROGRESS|COMPLETE|INCOMPLETE
lesson: <Lesson/Unit/Day>
checkpoints: 10 <✅/❌> | 20 <✅/❌> | 35 <✅/❌> | 44 <✅/❌>
deliverables:
- <...>
incorrect_count: <n>
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
subject: <Subject Name>
status: NOT_STARTED|IN_PROGRESS|COMPLETE|INCOMPLETE
lesson: <Lesson/Unit/Day>
checkpoints: 10 <✅/❌> | 20 <✅/❌> | 35 <✅/❌> | 44 <✅/❌>
deliverables:
- <...>
incorrect_count: <n>
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
subject: <Subject Name>
status: NOT_STARTED|IN_PROGRESS|COMPLETE|INCOMPLETE
lesson: <Lesson/Unit/Day>
checkpoints: 10 <✅/❌> | 20 <✅/❌> | 35 <✅/❌> | 44 <✅/❌>
deliverables:
- <...>
incorrect_count: <n>
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
subject: <Anchor Subject>
status: NOT_STARTED|IN_PROGRESS|COMPLETE|INCOMPLETE
lesson: <Lesson/Unit/Day>
checkpoints: 10 <✅/❌> | 20 <✅/❌> | 35 <✅/❌> | 44 <✅/❌>
deliverables:
- <...>
incorrect_count: <n>
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
subject: <Elective or Extra>
status: NOT_STARTED|IN_PROGRESS|COMPLETE|INCOMPLETE
lesson: <Lesson/Unit/Day>
checkpoints: 10 <✅/❌> | 20 <✅/❌> | 35 <✅/❌> | 44 <✅/❌>
deliverables:
- <...>
incorrect_count: <n>
score: <0-100>
letter: <A|B|C|D|F>
deductions:
- <...>
next_fix:
- <...>
carryover:
- <...>

<!-- /MODULE -->


<!-- MODULE: school.log.current.M90 | name="Auto-Increment Rule (behavior contract)" -->

## Auto-Increment Rule (behavior contract)

On `SCHOOL:START` when this log is loaded:
- If `school.last_date` is not today:
  - increment `school.day_number` by 1
  - set `school.last_date` to today
  - set `today.day_number` to new day number
  - set `today.school_complete=false`
  - reset all class blocks to `NOT_STARTED` and clear lesson/deliverables/scores
- If `school.last_date` is today:
  - do not increment; resume the day

<!-- /MODULE -->
