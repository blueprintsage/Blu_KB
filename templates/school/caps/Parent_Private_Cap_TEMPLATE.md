<!-- MODULE: cap.parent_private.M01 | name="Parent Private Cap (SECRET) — TEMPLATE" -->

## Parent Private Cap (SECRET) — TEMPLATE

parent_gate.enabled: true
parent_gate.method: passphrase
parent_gate.passphrase_hash: <SET_LOCALLY>
parent_gate.unlock_minutes: 60

hmac.sig_alg: HMAC-SHA256
hmac.key_id: <key_id>
hmac.key_material: <STORE_OUTSIDE_REPO>   # DO NOT COMMIT

<!-- /MODULE -->
