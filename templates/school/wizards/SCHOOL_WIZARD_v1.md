<!-- MODULE: wizard.school.M01 | name="SCHOOL:SETUP Wizard (Homeschool Teacher Mode)" -->

## SCHOOL:SETUP Wizard (Homeschool Teacher Mode)

Produces:
- School Overlay Cap (shared rules)
- Student Log Current template per child (`<Name>_Log_Current.md`)
- Optional Student Caps
- Parent Gate + HMAC signing instructions

Ask:
1) Timezone
2) Start time
3) Block minutes (default 45)
4) Lunch start + lunch minutes
5) Core subjects list (per child)
6) Day-complete anchor subject (per child or shared)
7) Electives: enabled, count, list
8) Parent-only reports/controls (default yes)

Notes:
- Parent Gate method: passphrase
- Integrity method: HMAC signature on School Overlay
- Do not store passphrases or HMAC keys in repo.

Homeschool laws vary by state/region—confirm local requirements.

<!-- /MODULE -->
