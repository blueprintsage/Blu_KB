# DP-VIS-001 Visual Prompting & Image Generation
**Scope:** Turning a visual spec into robust prompts, iterating via deltas, controlling composition/lighting.

### Schema
**Required**
- Subject + action
- Style target (photoreal / illustration / cinematic / etc.)
- Composition (shot size, angle, framing)
- Lighting (key, mood, time of day)
- Environment/background
- Must-have (3) / Must-avoid (3)

**Optional**
- Camera/lens language (e.g., 35mm, shallow DOF)
- Color mood (warm/cool/contrast)
- Textures/material cues
- Negative prompt list

### Checks
- [ ] Prompt includes **subject + setting + composition + lighting** (all 4).
- [ ] Must-haves are explicitly stated and not contradicted.
- [ ] Must-avoids are expressed as negatives (when supported) or as positive constraints.
- [ ] Iterations use **prompt deltas** (only change what knob changed).
- [ ] Output remains consistent with intended style (no accidental style drift).

### Failure-modes
- “Subject looks wrong” → missing concrete descriptors → add age/shape/material/pose specifics.
- “Busy clutter” → weak composition constraint → add foreground/background separation + framing note.
- “Wrong lighting mood” → vague lighting → specify key direction + softness + time-of-day cues.
- “Style drift” → too many changes per iteration → isolate one knob per iteration.
- “Artifacts / weird anatomy” → insufficient constraints → add realism anchors + simplify pose.

### Knobs
- Realism (illustrative ↔ photoreal)
- Lens/DOF (deep focus ↔ shallow)
- Lighting mood (soft ↔ harsh; golden hour ↔ overcast)
- Composition (centered ↔ rule-of-thirds; wide ↔ close)
- Texture richness (minimal ↔ detailed)
- Background complexity (clean ↔ busy)
- Color grade (neutral ↔ cinematic)
- Iteration mode (one-knob-at-a-time ↔ batch)


### Working Patterns
**PAT-VIS-001 Prompt Skeleton (4-core)**
- **Use when:** prompts keep missing intent.
- **Steps:** subject → setting → composition → lighting → must/avoid list.
- **Checks:** includes all 4; must-haves not contradicted.
- **Failure-modes:** generic results → add concrete descriptors (materials, pose, era).
- **Knobs:** realism; lens; background complexity.

**PAT-VIS-002 One-Knob Iteration**
- **Use when:** outputs drift.
- **Steps:** choose one knob → state delta → regenerate → compare to checks.
- **Checks:** only one variable changed; style consistent.
- **Failure-modes:** multiple changes creep in → restate “only change X”.
- **Knobs:** any knob list.

### Drills
- **DRL-VIS-001 (10 min):** Write a prompt using the 4-core skeleton + 5 knobs.
- **DRL-VIS-002 (15 min):** Run 3 iterations: change one knob each time; keep checks fixed.

### Minimal Example (micro-output)
Prompt skeleton:
- “Photoreal portrait of [subject], [pose], [environment], [lighting], [lens/DOF], [mood]. Must: __. Avoid: __.”
**Checks:** includes 4 core elements; must-have list present.

---
