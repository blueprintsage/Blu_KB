<!--
Blu Repo Bootstrap README (module-style, paste-safe)
No YAML front matter on purpose (Notepad++ copy/paste friendliness).
-->

# Blu-KB Repo — Skillsets DB (Bootstrap)

<!-- MODULE: repo.M00 | name="Scope Lock" -->
## Scope Lock (hard boundary)
This repo contains **ONLY**:
- **DPs (Domain Packs)** — teaching/reference docs
- **PDs (Patterns & Drills)** — repeatable practice exercises (**stored inside their specific sub-skill folders**)
- **Reference assets** for image/video generation (refs, moodboards, palettes, storyboard templates, etc.)

This repo contains **NO**:
- Blu core capsules (Persona / Anchors / Matrix / Workbench / etc.)
- Personal info, family memories, private identifiers

Repo usage: **OFF by default**. It’s an optional DB when explicitly enabled.
<!-- /MODULE -->

<!-- MODULE: repo.M01 | name="Definitions" -->
## Definitions
- **DP** = Domain Pack (learn/reference binder)
- **PD** = Patterns & Drills (practice)
- **Assets** = reference-only materials (track provenance/license when possible)
<!-- /MODULE -->

<!-- MODULE: repo.M02 | name="Directory Layout" -->
## Directory Layout (skillsets-first)
```
/index/
  MASTER_INDEX.md
  ASSET_INDEX.md

/skills/
  gamedev/
    index.md
    gdd/
      dp/
      pd/
    engines/
      unreal/
        dp/
        pd/
      godot/
        dp/
        pd/
  writing/
    index.md
    editing/
      dp/
      pd/
    creative/
      dp/
      pd/
    resume/
      dp/
      pd/
  art/
    index.md
    image_gen/
      prompts/
      refs/
      pd/
    video_gen/
      prompts/
      refs/
      pd/
    storyboarding/
      templates/
      examples/
      pd/
    comics/
      refs/
      lettering/
        pd/
      panels/
        templates/
```

**Rule:** PDs live under the subfolder they train (to avoid getting lost).
<!-- /MODULE -->

<!-- MODULE: repo.M03 | name="Naming Conventions" -->
## Naming Conventions
DPs: `DP-<SKILL>-<SUB>-###.md`  
PDs: `PD-<SKILL>-<SUB>-###.md`

Assets:
- Images: `IMG-<THEME>-####.(png|jpg|webp)`
- Video refs: `VID-<THEME>-####.(mp4|mov|gif)`
- Optional sidecar metadata: same name + `.yml` (see templates)

Examples:
- `DP-WRIT-EDIT-001.md`
- `PD-GAME-UE-003.md`
- `IMG-noir-0007.webp` + `IMG-noir-0007.yml`
<!-- /MODULE -->

<!-- MODULE: repo.M04 | name="Statuses (optional)" -->
## Statuses (optional)
`INTAKE → DRAFT → ACTIVE → DEPRECATED`

Prefer **deprecate** over delete.
<!-- /MODULE -->

<!-- MODULE: repo.M05 | name="Indexing Rules" -->
## Indexing Rules
- `/index/MASTER_INDEX.md` links to each skill’s local `index.md`
- `/index/ASSET_INDEX.md` catalogs assets (or assets use sidecar `.yml`)
- Every DP/PD should be discoverable from a local index
<!-- /MODULE -->

<!-- MODULE: repo.M09 | name="Bootstrap Checklist" -->
## Bootstrap Checklist
- [ ] Create folders under `/skills/` for your skillsets
- [ ] Create a local `index.md` per skillset
- [ ] Start with 1 DP + 1 PD in a single subfolder
- [ ] Add assets only with provenance/license notes
<!-- /MODULE -->

*Last updated:* 2026-02-15
