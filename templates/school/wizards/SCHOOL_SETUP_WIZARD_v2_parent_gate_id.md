module: blu__school.M02 | name="SCHOOL:SETUP Wizard (with Parent Gate ID) | status=active"

# SCHOOL:SETUP Wizard (with Parent Gate ID)

**Design goal:** one question at a time (no big paste blocks), outputs downloadable markdown files.

## Steps (one at a time)
1) Timezone
2) Start time
3) Block minutes
4) Lunch start
5) Lunch minutes
6) Student name
7) Core subjects
8) Anchor subject
9) Parent lock? (Yes/No)
   - If Yes: ask for `parent.gate.id` (default: `PGK-<STUDENT>-01`)

## Outputs
Always:
- `School_Overlay.md`
- `<Student>_Log_Current.md`

If Parent lock enabled:
- Provide `Parent_GOD_Mode_Key_TEMPLATE.md`
- Ask for hash OR instruct hash generation method (website/local)
- Optionally generate `Parent_GOD_Mode_Key.md` once hash is provided

/module
