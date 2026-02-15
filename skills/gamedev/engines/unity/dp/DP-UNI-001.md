# DP-UNI-001 Unity Gameplay & Debugging
**Scope:** Unity engine gameplay systems, architecture, debugging workflows, and performance hygiene (C#).

### Schema
**Required**
- Unity version + target platform
- Feature goal (movement/UI/save/combat/etc.)
- Current behavior vs desired behavior
- Constraints (feel targets, perf, input scheme)

**Optional**
- Minimal repro scene plan
- Relevant scripts (snippets) + errors/logs
- Package context (Input System vs old input, URP/HDRP, etc.)

### Checks
- [ ] Works in a minimal repro scene.
- [ ] Inputs are mapped and verified.
- [ ] State transitions are explicit (no magic booleans everywhere).
- [ ] Profiling sanity pass completed (CPU/GPU spikes identified).
- [ ] Build test passes (not just Editor).

### Failure-modes
- “Works in Editor, breaks in build” → missing assets/stripping/settings → add build checks + logs.
- “Random null refs” → lifecycle order + missing refs → validate in Awake/OnEnable; add guards.
- “Janky movement” → mixing Update/FixedUpdate → move physics to FixedUpdate.
- “GC spikes” → per-frame allocations → cache refs; avoid LINQ in hot paths.
- “Input not firing” → wrong system/settings → verify Input System package + project settings.

### Knobs
- Architecture (quick script ↔ componentized)
- Debug verbosity (none ↔ overlay)
- Perf focus (readable ↔ optimized)
- Input system (legacy ↔ new)
- Test depth (smoke ↔ thorough)

---
