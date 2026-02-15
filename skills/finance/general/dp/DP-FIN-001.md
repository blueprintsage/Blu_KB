# DP-FIN-001 Finance & Econ Explainers
**Scope:** Explain concepts, summarize news drivers, interpret indicators—**not** personalized financial advice.

### Schema
**Required**
- Topic or question
- Time window (e.g., “this week”, “since 2020”)
- Audience level (beginner/intermediate/advanced)
- Desired output (explainer / glossary / what-to-watch)

**Optional**
- Data series to reference
- Regions/sectors
- Risk framing (optimistic/neutral/skeptical)

### Checks
- [ ] Facts vs interpretation are labeled.
- [ ] Uncertainty is stated; no predictions framed as certainty.
- [ ] If referencing current info, sources are cited.
- [ ] Output includes “what would change my view” (2–4 bullets) when relevant.

### Failure-modes
- “Sounds like advice” → too directive → reframe as scenarios + risks + questions.
- “Too jargon-y” → level mismatch → add definitions and one example.
- “Outdated” → no recency check → refresh via sources; include dates.
- “Overconfident” → missing uncertainty → add caveats + alternative hypotheses.

### Knobs
- Level (beginner ↔ advanced)
- Tone (neutral ↔ skeptical)
- Depth (overview ↔ deep dive)
- Output type (bullet explainer ↔ narrative)
- Focus (macro ↔ sector ↔ company)

---

### Working Patterns
**PAT-FIN-001 Facts vs Interpretation Split**
- **Use when:** topic could be mistaken for advice.
- **Steps:** list facts (with dates) → list interpretations → list scenarios/risks → “what would change my view”.
- **Checks:** facts are sourced; interpretations labeled.
- **Failure-modes:** too confident → add alternative hypothesis.
- **Knobs:** skepticism; depth; audience level.

### Drills
- **DRL-FIN-001 (10 min):** Explain one indicator (CPI/jobs/rates) with 3 checks and one example.
- **DRL-FIN-002 (15 min):** Summarize a week of market drivers: 5 facts + 3 interpretations + 2 scenarios.
---


# Cross-Pack Pattern Library

## PAT-TPL-001 Pattern Template (copy/paste)
- **ID:** PAT-<AREA>-###
- **Use when:** …
- **Schema:** (inputs/constraints)
- **Steps:** 1…2…3…
- **Checks:** 2–5 observable pass criteria
- **Failure-modes:** Symptom → Cause → Fix (3–6)
- **Knobs:** 6–10 user-invokable toggles

## DRL-TPL-001 Drill Template (copy/paste)
- **ID:** DRL-<AREA>-###
- **Tier:** Beginner | Intermediate | Advanced
- **Prompt:** …
- **Timebox:** 5–15 min
- **Pass criteria:** …
- **Common misses:** …
- **Answer sketch (optional):** …


## PAT-CORE-001 Deliverable-First Output
**Use when:** user wants something they can paste/run/ship.  
**Recipe:** Deliverable → Checks → Failure-modes → Knobs → Next.

## PAT-CORE-002 Prompt Delta Iteration
**Use when:** iterating on prompts, prose, or specs.  
**Rule:** change one knob per iteration; show the delta explicitly.

## PAT-CORE-003 Completeness Rule
**Use when:** required section is missing/thin.  
**Rule:** re-export the whole output in the correct structure; don’t patch with one line.

## PAT-CORE-004 Micro-Demo
**Use when:** authoring a new pack.  
**Rule:** include ≤200 words (or ≤40 lines code) example + ≥2 checks.

---

# Backlog / Next Packs
- DP-WEB-001 Web/App Dev (React + APIs + debugging)
- DP-DATA-001 Spreadsheets & analysis workflows
- DP-OPS-001 Personal productivity / task systems
- DP-EDU-001 Lesson plan generator (multi-level scaffolding)
