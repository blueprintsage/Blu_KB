# DP-GDD-001 Game Design Docs
**Scope:** Game design documents, feature specs, scope control, and “ship-ready” acceptance tests.

### Schema
**Required**
- Pillars (3) + target player fantasy
- Core loop (minute-to-minute)
- Progression (short/mid/long-term)
- Key systems list (combat, economy, crafting, etc.)
- Scope constraints (team size/time/engine)

**Optional**
- Content budget (levels/enemies/items count)
- Economy numbers (placeholder ranges)
- UX flow (menus, onboarding)
- Risks + mitigations

### Checks
- [ ] Every system ties back to a pillar.
- [ ] Core loop is playable in a prototype (MVP defined).
- [ ] Progression has clear goals and feedback.
- [ ] Each feature has acceptance tests (observable).
- [ ] Scope matches constraints (no hidden “MMO” scope).

### Failure-modes
- “Too big to ship” → scope creep → define MVP + cut list.
- “No reason to keep playing” → weak progression → add goals, unlocks, mastery hooks.
- “Systems conflict” → missing invariants → define rules (e.g., economy sinks/sources).
- “Unclear audience” → vague pillars → rewrite pillars as player promises.
- “Design can’t be implemented” → no constraints → add engine/time limits early.

### Knobs
- Scope (MVP ↔ full)
- Detail level (one-pager ↔ full doc)
- Numbers (none ↔ placeholder ranges)
- Risk tolerance (safe ↔ experimental)
- Format (bullets ↔ sections ↔ tables)

---


## Visual AI
