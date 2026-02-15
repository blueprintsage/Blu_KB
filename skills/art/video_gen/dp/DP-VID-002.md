# DP-VID-002 Text-to-Video Prompting & Iteration
**Scope:** Tool-agnostic prompting for text-to-video models (e.g., Sora-style), with controlled iteration and artifact control.

### Schema
**Required**
- Subject + action (what changes over time)
- Setting + constraints (indoors/outdoors, time of day)
- Camera spec (angle, distance, movement style)
- Duration + aspect ratio
- Must-have (3) / Must-avoid (3)

**Optional**
- Beat timing (0–2s / 2–4s / 4–6s)
- Lens/DOF language (wide/tele, shallow/deep)
- Motion strength (low/med/high), stabilization (off/on)
- Negative list (logos/text/weird hands/etc.)

### Checks
- [ ] Prompt includes **subject, action, camera, setting** (all 4).
- [ ] Temporal clarity: viewer can describe what happens **each 2 seconds**.
- [ ] Must-avoids are explicit (logos/text/watermarks/hands, etc.).
- [ ] Iteration uses **one knob per run** (no drift).
- [ ] No unwanted new subjects appear (duplicates, extra limbs, extra people).

### Failure-modes
- “Melting rooms / warping geometry” → too much motion + complex environment → reduce motion, simplify background, shorten duration.
- “Jitter/flicker” → unstable camera instruction → specify continuous take + stabilization OR milder handheld.
- “Duplicate subject” → unclear subject identity → “single [subject] only” + exclude duplicates.
- “Weird hands/people” → model invents humans → “no humans in frame” + add hands/limbs to negatives.
- “Action unclear” → vague verbs → add path + milestones (“down hall, left turn, under table…”).

### Knobs
- Camera (handheld ↔ stabilized)
- Motion blur (low ↔ strong)
- Environment detail (clean ↔ busy)
- Duration (4s ↔ 10s)
- Realism (stylized ↔ photoreal)
- Beat density (simple ↔ complex)
- Negative strictness (light ↔ heavy)

---

