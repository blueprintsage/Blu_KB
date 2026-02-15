# DP-GOD-001 Godot 4.x Gameplay & Debugging
**Scope:** Node/scene architecture, GDScript gameplay features, debugging and migration discipline.

### Schema
**Required**
- Goal feature (movement / dash / UI / save / etc.)
- Godot version (4.x) + target platform
- Scene context (which nodes exist; player controller type)
- Inputs (actions and mappings)
- Constraints (feel targets: speed, cooldown, camera)

**Optional**
- Minimal Repro Scene plan
- Signals/events expected
- Performance constraints

### Checks
- [ ] Feature works in a **minimal repro scene** (no unrelated dependencies).
- [ ] Inputs are mapped and tested (pressed/just_pressed, etc.).
- [ ] State transitions are explicit (e.g., Idle → Dash → Recover).
- [ ] Timers/cooldowns are deterministic (no frame-rate dependence).
- [ ] Debug output (prints or on-screen) validates state and key vars.

### Failure-modes
- “Dash cancels randomly” → state overwritten by movement code → gate movement during dash state.
- “Speed varies with FPS” → using `_process` for physics → move to `_physics_process` + delta usage.
- “Input doesn’t fire” → action not mapped → check Project Settings input map.
- “Player clips walls” → no collision handling → use move_and_slide + collision checks.
- “Hard to debug” → no minimal repro → extract to a tiny scene with just the player + collider.

### Knobs
- Movement feel (snappy ↔ floaty)
- Dash distance (short ↔ long)
- Dash invulnerability (off ↔ on)
- Cooldown (none ↔ long)
- Camera behavior (locked ↔ follow ↔ damped)
- Debug verbosity (none ↔ prints ↔ on-screen overlay)
- Architecture (monolith ↔ component nodes ↔ data-driven)


### Working Patterns
**PAT-GOD-001 State Gate for Abilities**
- **Use when:** movement/abilities conflict.
- **Steps:** define states → gate input per state → transition rules → timers in physics.
- **Checks:** no overlapping states; deterministic end conditions.
- **Failure-modes:** state overwritten → centralize state updates.
- **Knobs:** dash duration; cooldown; control lock.

**PAT-GOD-002 Minimal Repro Scene**
- **Use when:** bug is hard to reproduce.
- **Steps:** new scene → player + one collider → reproduce → add debug prints.
- **Checks:** bug reproduces in isolation; fix verified.
- **Failure-modes:** dependencies missing → stub them.
- **Knobs:** repro complexity; debug verbosity.

### Drills
- **DRL-GOD-001 (10 min):** Build a minimal dash state machine sketch + 3 checks.
- **DRL-GOD-002 (15 min):** Create a minimal repro plan for a physics bug + what to log.

### Minimal Example (micro-output)
State machine sketch:
- Variables: `is_dashing`, `dash_timer`, `dash_dir`
- Checks: dash ends after duration; cooldown prevents retrigger.

---
