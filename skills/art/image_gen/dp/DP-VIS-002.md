# DP-VIS-002 Image Enhancement & Hyper-Real Edits
**Scope:** “Make it more realistic” while preserving composition/identity—minimal-delta enhancement, artifact cleanup, and targeted edits.

### Schema
**Required**
- Source image(s)
- Must-keep list (pose, outfit, background, composition, etc.)
- Must-change list (exact features to edit)
- Realism target (DSLR photo / game cinematic / studio portrait)

**Optional**
- Reference image(s) for realism/lighting
- Skin/texture preference (subtle ↔ detailed)
- Makeup spec (liner, shadow, lipstick shade)
- Material spec (metal type, emissive color, roughness)

### Checks
- [ ] Must-keep items are preserved (composition, pose, clothing).
- [ ] Only requested features change (no “bonus” implants/logos).
- [ ] Skin/eyes/materials read physically plausible (no plastic skin).
- [ ] No text/logos/watermarks introduced.
- [ ] Face identity remains consistent (no “face drift”).

### Failure-modes
- “Model changes outfit/background” → must-keep list too weak → restate “do not change X” + simplify prompt.
- “Over-smoothing / wax skin” → realism too aggressive → ask for “micro-texture, pores, peach fuzz.”
- “Adds extra tech around eye” → ambiguous cybernetic spec → specify “metallic sclera only; no orbital plating.”
- “Color drift” → vague palette → lock key colors (hair, iris, lipstick).
- “Identity drift” → too many changes → one-knob iteration + keep seed if possible.

### Knobs
- Delta size (minimal ↔ bold)
- Skin detail (subtle ↔ high micro-texture)
- Lighting (soft ↔ dramatic)
- Lens (35mm ↔ 85mm portrait)
- Background (unchanged ↔ softened bokeh)
- Makeup intensity (natural ↔ dramatic)

---


## Video
