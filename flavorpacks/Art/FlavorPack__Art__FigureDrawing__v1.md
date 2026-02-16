---
type: FlavorPack
domain: Art
pack: FigureDrawing
version: v1
status: canon-candidate
created: 2026-02-16
tags: [flavorpack, art, drawing, figure, anatomy, gesture, construction, lineart]
triggers:
  keywords: ["draw", "sketch", "figure", "pose", "anatomy", "gesture", "hands", "head", "creature", "foreshortening"]
  commands: ["CMD:DRAW", "CMD:FIGURE"]
defaults:
  flow: "Workshop"
  output_shape: ["TL;DR", "Steps", "Gotchas", "Checks", "Next"]
  token_budget: tight
ruleset:
  must:
    - "Use Stick → Block → Rough → Final explicitly for drawing/organic forms."
    - "End each stage with a pass/fail Success Check."
    - "Prioritize action/readability before anatomy detail."
  never:
    - "Do not finalize lines in Stick/Block/Rough."
    - "Do not name muscles unless user asks."
    - "Do not flood with options when user is overwhelmed."
---

# FlavorPack — Art — Figure Drawing (Stick / Block / Rough / Final) v1

## TL;DR
We build a readable pose first (**Stick**), give it volume and depth (**Block**), refine landmarks and anatomy (**Rough**), then commit to clean, chosen lines (**Final**). Each stage ends with a pass/fail check.

---

## Steps

## 0) Intake (Goal + Constraints)
**Goal (what are we drawing?):**
- subject: human / creature / hybrid / animal / alien
- action: running / jumping / reaching / punching / falling / twisting
- view: front / side / 3-4 / top / low angle
- timebox: 30s / 1m / 5m / 15m
- medium: pencil / ink / digital lineart
- style target: realistic / comic / stylized / dynamic

**Constraints (pick only what matters):**
- silhouette clarity: Y/N
- depth/foreshortening: Y/N
- anatomy accuracy: basic / intermediate / advanced
- line weight: flat / near-heavy / tapered
- camera distance: close-up / full body

**Output:**
- 4-panel progression (Stick/Block/Rough/Final) **or**
- single final line art **or**
- drill plan (reps + checks) **or**
- critique rubric

---

## 1) Primary Pipeline (for drawing / organic forms)

### Stage 1 — STICK (Gesture / Intent)
**Do:**
- one clear line of action
- head = egg/circle
- spine = one line
- limbs = straight lines + joint dots
- chest mass = oval
- hips mass = box/oval (tilt matters)
- hands = small circle, feet = triangle

**Don’t:**
- no anatomy, no cleanup, no fingers/toes

**Success Check (pass/fail):**
- From 6 feet away: can someone name the action in 2 seconds?

---

### Stage 2 — BLOCK (Volume / Depth)
**Do:**
- limbs into cylinders/boxes (show orientation)
- overlap shapes to show depth (near in front)
- foreshorten by size (near bigger, far smaller)
- establish ribcage vs pelvis tilt
- neck = short cylinder
- hands/feet: mitten wedge + foot wedge

**Don’t:**
- no muscle detail yet
- no “pretty” contours—only forms

**Success Checks (pass/fail):**
- Overlap: do near forms clearly sit in front of far forms?
- Scale: do size shifts match distance?

---

### Stage 3 — ROUGH (Landmarks / Mechanics)
**Do:**
- refine contours from the forms
- place major landmarks (simple):
  - collar line / sternum line
  - pelvis “handles” (front hip points)
  - elbows/knees as hinge landmarks
- simplify muscles as masses (no naming required)
- face planes if needed (brow / nose wedge / jaw plane)

**Don’t:**
- don’t ink/commit yet
- avoid tiny detail unless the pose demands it

**Success Checks (pass/fail):**
- Balance: center of mass reads supported by the base?
- Landmarks: do elbows/knees land where the cylinders imply?

---

### Stage 4 — FINAL (Line Selection / Clarity)
**Do:**
- reject weak lines; keep only chosen contours
- emphasize silhouette + key overlaps
- line weight: near edges heavier, far lighter
- keep edges purposeful (curves for flow, straights for structure)

**Don’t:**
- don’t re-solve anatomy here
- don’t add shading texture in a line-art pass

**Success Checks (pass/fail):**
- Readability: silhouette reads instantly
- Depth: overlaps still obvious without earlier layers
- Confidence: lines look chosen, not searched

---

## Gotchas (and fixes)
- **Stiff mannequin:** you blocked before the pose reads.  
  Fix: redo Stick until action is obvious; then block.
- **Flat figure:** no overlap, no size shift.  
  Fix: exaggerate overlap and scale (near bigger).
- **Over-detail too early:** fingers/toes in Stage 1–2.  
  Fix: mitten + wedge only until Rough.
- **Hairball final:** too many “maybe” lines.  
  Fix: final pass is line *selection*, not exploration.

---

## Checks (quick rubric)
Score 0–2 each:
- Action readability (Stick)
- Depth/overlap (Block)
- Balance/landmarks (Rough)
- Line confidence (Final)
- Overall clarity

**One-fix rule:** improve the lowest score only on the next rep.

---

## Next (Drill Packs)

### A) 10-Min Readable Action Drill (Beginner)
- 5 poses × 1 minute each: running, jumping, reaching, punching, falling
- Round 1: Stick only
- Round 2: Stick + chest/hips ovals (still 1 minute each)

**Success Check:** can another person name each action without hints?

---

### B) Z-Axis Foreshortening Drill (Depth Core)
- Day 1: cylinders pointing toward viewer (3 angles)
- Day 3: punch/kick toward camera
- Day 7: torso twist + crossing limb

**Success Checks:** overlap + scale (pass/fail)

---

### C) Silhouette First (Clarity Under Chaos)
- pick 3 dynamic poses
- Stage 4 starts with silhouette-only, then interior lines

**Success Check:** silhouette reads when filled solid black

---

## High-Velocity Variant (Engine Only)
If user appends `--` or says “Just the gears”:
1) Stick: line of action + joints (no detail)  
2) Block: cylinders + overlaps (near bigger)  
3) Rough: landmarks + masses (no names)  
4) Final: choose lines + weight overlaps  
**Check:** “Does the action read instantly? (Y/N)”  
**Next:** repeat the same pose once with bigger overlap/scale.

---

## Provenance Footer
Sources: Hogarth-inspired construction + Admin-taught 4-stage workflow (sanitized)  
Date added: 2026-02-16  
Status: canon-candidate  
Modifications: v1 initial standard FlavorPack format  
