# DP-WRI-005 Summarization
**Scope:** Turn transcripts/articles into structured summaries, study notes, or action plans.

### Schema
**Required**
- Source text (or transcript)
- Summary type (bullets / study notes / action plan)
- Length target
- Audience level (beginner ↔ expert)

**Optional**
- Key questions to answer
- “Extract quotes” (if allowed)
- Output format (markdown, table, etc.)

### Checks
- [ ] Captures main thesis + supporting points.
- [ ] Separates facts vs opinions (when present).
- [ ] Includes action items (if requested).
- [ ] No invented claims.

### Failure-modes
- “Too long” → unclear length target → set word/section limit.
- “Too shallow” → missing key questions → add 3 questions and re-summarize.
- “Missed nuance” → source too long → chunk + stitch with section headers.

### Knobs
- Compression (tight ↔ detailed)
- Structure (bullets ↔ narrative)
- Focus (general ↔ answer questions)
- Tone (neutral ↔ friendly)


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
