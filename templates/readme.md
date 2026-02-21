<!-- MODULE: blu__templates.01 | name="Templates README" -->

# Templates

Canonical templates used by Blu (docs, headers, art boards, etc.).  
Prefer adding reusable templates here over one-off copies elsewhere.

## Rules (house standard)
- Keep templates modular + reusable.
- Use consistent naming (see `templates/_meta/naming_rules.md`).
- Add new templates to `templates/_meta/template_index.md` so they’re discoverable.
- Prefer **repo paths** (not chat-local) when referencing templates.

## Structure (recommended)
templates/
  _meta/
    template_index.md
    naming_rules.md
  docs/
    Capsule_Header_Template.md
    (optional copies of doc scaffolds)
  art/
    comics/
      boards/

## Key templates
- Module wrapper — `templates/docs/module_block.md`
- Capsule header — `templates/docs/Capsule_Header_Template.md`
- Comic boards — `templates/art/comics/boards/`

## Comic boards support note
- Preferred / supported default: use the PNG board files (reliable via GitHub UI + raw).
- Optional: PDF boards may be present for print workflows, but some environments/tools may not fetch raw PDFs reliably.

<!-- /MODULE -->

Note: If raw.githubusercontent.com appears stale, use GitHub UI or add a cache-bust query (?v=<commit>).