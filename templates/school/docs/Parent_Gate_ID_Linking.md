<!-- MODULE: blu__school_docs.M03 | name="Parent Gate ID (How Linking Works) | status=active" -->

# Parent Gate ID (How Linking Works)

To keep parent secrets out of student files, we use a **Gate ID** pointer.

- The **Parent Key** file contains:
  - `parent.gate.id` (identifier)
  - `parent.gate.hash` (the hash)

- The **School Overlay** and/or **Student Log** contain only:
  - `parent.gate.required: true`
  - `parent.gate.id: <same id>`

Blu allows parent-only commands only when:
1) the Parent Key is loaded,
2) `PARENT:UNLOCK` succeeds, and
3) the `parent.gate.id` values match.

This makes rotation easy (change hash, keep the same ID) and avoids spreading hashes around.

<!-- /MODULE -->
