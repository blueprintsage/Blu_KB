# DP-CODE-001 Code Development
**Scope:** Building/debugging scripts, apps, automations; producing runnable code + reproducible troubleshooting.

### Schema
**Required**
- Goal (feature / fix / script purpose)
- Language/runtime + versions
- OS + environment (paths, permissions, package manager)
- Inputs/outputs (sample I/O)
- Constraints (time, safety, idempotence, performance)

**Optional**
- Existing code snippet or repo structure
- Error text/logs + expected behavior
- Test data + edge cases

### Checks
- [ ] Steps are copy/paste runnable (commands, paths, expected output).
- [ ] Includes at least 2 tests (happy path + one edge case).
- [ ] Error handling is explicit (what fails, how it reports, exit codes/exceptions).
- [ ] If destructive actions exist, they are called out and guarded (confirmations/backups/dry-run).

### Failure-modes
- “Doesn’t work on my machine” → missing environment details → add version/path/permission checks + exact install steps.
- “Fix breaks something else” → no tests/regression check → add minimal test script + before/after expected outputs.
- “Hard to debug” → no minimal repro → extract to minimal repro file + log key variables.
- “Silent failure” → swallowed exceptions → re-raise with context + structured error messages.

### Knobs
- Verbosity (minimal ↔ fully commented)
- Safety (dry-run ↔ live)
- Style (quick hack ↔ production-ready)
- Dependency footprint (stdlib-only ↔ allowed libs)
- Logging (none ↔ debug)
- Output format (human ↔ JSON/CSV)
- Test depth (smoke ↔ thorough)

### Working Patterns
**PAT-CODE-001 Minimal Repro Scaffold**
- **Use when:** bug report is vague or entangled with a big project.
- **Steps:** isolate smallest script → hardcode sample input → reproduce error → add 2 checks.
- **Checks:** repro script runs in clean env; error occurs consistently.
- **Failure-modes:** still too big → keep deleting until failure disappears, then re-add last change.
- **Knobs:** repro size; logging level; input complexity.

**PAT-CODE-002 Validate Inputs Before Work**
- **Use when:** scripts crash mid-run or corrupt data.
- **Steps:** parse → validate types/ranges → fail fast with message → proceed.
- **Checks:** invalid input exits cleanly; valid input proceeds.
- **Failure-modes:** validation too strict → add “lenient mode” knob.
- **Knobs:** strictness; default values; error detail.

**PAT-CODE-003 Wrap Risky Calls With Clear Errors**
- **Use when:** external IO (network/files) fails unpredictably.
- **Steps:** try/except → attach context → retry/backoff (optional) → surface actionable message.
- **Checks:** error includes operation + path/url; retry count bounded.
- **Failure-modes:** infinite retries → cap + escalate.
- **Knobs:** retries; timeout; backoff.

### Drills
- **DRL-CODE-001 (10 min):** Turn a vague bug (“it crashes”) into a minimal repro + 2 checks.
- **DRL-CODE-002 (15 min):** Add logging + input validation to an existing snippet; show one failing and one passing run.
