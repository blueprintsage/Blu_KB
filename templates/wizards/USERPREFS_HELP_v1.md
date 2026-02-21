# Userprefs Help (v1)
Last updated: 2026-02-21
tz: America/Chicago
status: active

Find: help userprefs prefs usercap patch reset wizard

module: templates.wizards.USERPREFS_HELP_v1.M01 | name="What are userprefs?"
Userprefs are durable settings that control tone, time handling, repo usage, teaching style, and task cadence.
They live under `usercap_v1.prefs`.
/module

## Common requests
Find: setup update show reset export

module: templates.wizards.USERPREFS_HELP_v1.M02 | name="Help menu"
- “Run userprefs wizard”
- “Show my current prefs”
- “Update prefs: <key>=<value>”
- “Reset prefs”
- “Export prefs”
/module

## Key map
Find: keys identity timezone dates tone repo teach tasks

module: templates.wizards.USERPREFS_HELP_v1.M03 | name="Prefs reference"
identity.display_name
identity.pronouns (optional)

timezone (IANA)
datefmt (YYYY-MM-DD recommended)
rel_dates (always+absolute recommended)

tone (warm|neutral|formal)
verbosity (brief|normal|detailed)

teach.level (Beginner|Intermediate|Advanced)
teach.build_ladder (true|false)

repo.enabled (true|false)
repo.entrypoint_raw
repo.rules_doc
repo.prefer_commit_pinned (true|false)
repo.raw_cache_bust (true|false)
repo.module_sentinels.start ("module:")
repo.module_sentinels.end ("/module")

tasks.enabled (true|false)
tasks.cadence (offer_first_due_only|daily|weekly|manual)
/module

## Example patches
Find: examples yaml

module: templates.wizards.USERPREFS_HELP_v1.M04 | name="Examples"
Change timezone:
usercap_v1:
  prefs:
    timezone: "America/New_York"

Disable repo:
usercap_v1:
  prefs:
    repo:
      enabled: false
/module
