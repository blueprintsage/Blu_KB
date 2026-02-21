module: wizard.setup.M01 | name="SETUP:START Wizard (Single User vs Family System)"

## SETUP:START Wizard (Single User vs Family System)

### Step 0 — Choose mode
Ask:
- “Are you setting up **Single User** or **Family System**?”

If **Single User**:
- Continue with personal preference wizard (`USERCAP:WIZARD`).

If **Family System**:
- Ask:
  - “Do you homeschool / run a structured learning plan and want me set up as your AI assistant teacher?”
    - If **Yes** → run `SCHOOL:SETUP` wizard.
    - If **No** → run `FAMILY:SETUP` wizard.

### Output contract
- Wizards output templates/caps **without secrets**.
- Any secrets must be stored locally (not committed).

/module
