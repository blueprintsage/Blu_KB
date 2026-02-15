# DP-BP-001 Blueprint Scripting
**Scope:** UE-style Blueprint logic: exact node naming, wiring clarity, debugging flow, maintainable graphs.

### Schema
**Required**
- Engine version + context (Actor/Component/Widget)
- Graph location (Event Graph / Function / Macro)
- Inputs (events, parameters) + expected outputs
- Current behavior vs desired behavior
- Constraints (performance, replication, readability)

**Optional**
- Screenshots of graph
- Variable list (name, type, defaults)
- Data assets/tables involved

### Checks
- [ ] Uses exact node and pin names; specifies where actions happen in UI.
- [ ] Validates inputs early (null/empty/range) with explicit fail path.
- [ ] Debug plan included (prints/breakpoints/watches) for each branch.
- [ ] Graph intent is documented (comments on *why*, not *what*).

### Failure-modes
- “Wrong branch fires” → condition inverted or stale state → print values right before branch; verify exec flow.
- “Loop runs off-by-one” → unclear bounds → make bounds explicit; log index start/end.
- “Random null” → missing validation → add IsValid + fallback or early return.
- “Spaghetti graph” → hidden state and long wires → refactor into functions; expose inputs.

### Knobs
- Explicitness (beginner hand-holding ↔ expert terse)
- Debug instrumentation (none ↔ prints ↔ breakpoint-heavy)
- Refactor level (leave as-is ↔ split into functions)
- Data-driven (hardcoded ↔ struct/table-driven)
- Performance (readable ↔ optimized)

### Working Patterns
**PAT-BP-001 Validate → Branch → Handle Fail**
- **Use when:** runtime errors or nulls.
- **Steps:** IsValid → Branch → fail output (log + return) → success path.
- **Checks:** fail path triggers on null; success path unaffected.
- **Failure-modes:** fail path too noisy → add verbosity knob.
- **Knobs:** verbosity; fallback behavior.

**PAT-BP-002 Loop N Times With Clear Bounds**
- **Use when:** arrays/loops behave unexpectedly.
- **Steps:** define start/end → ForLoop → log index + item → break conditions.
- **Checks:** indexes match expectation; no out-of-range.
- **Failure-modes:** array changes during loop → copy array or iterate safely.
- **Knobs:** bound type (count vs last index); logging.

**PAT-BP-003 Data-Driven Selection (Struct/Table)**
- **Use when:** too many branches.
- **Steps:** define struct → lookup row → select fields → apply.
- **Checks:** row found; defaults applied if missing.
- **Failure-modes:** missing row → add fallback row.
- **Knobs:** fallback policy; table vs map.


**PAT-BP-004 Overlap Array Validity Guard (Run+Drop / Fast Movement)**
- **Use when:** A variable “randomly” becomes `None` during fast actions (run + drop, detach/attach, physics enabling), especially inside overlap/nearby-player loops.
- **Schema:** Inputs: `Overlaps/Players Array`, `Get Player Ref (Interface)`, `InteractingPlayer` (or similar). Assumption: array entries can become stale mid-frame.
- **Steps:** `IsValid(Array Element)` → Branch → (True) `Get Player Ref` → (recommended) `IsValid(Output)` → (True) `Set InteractingPlayer = Output`; otherwise skip. Never write `None` as a side effect of invalid input.
- **Checks:** (1) 20 consecutive run+drop attempts without unexpected clearing. (2) Invalid entries are skipped and do not affect state.
- **Failure-modes:** Still `None` → another setter exists (guard all); Output `None` → add `IsValid(Output)` + log; Multiplayer overwrite → move setter to authority/server.
- **Knobs:** Guard strictness; logging level; state-clear policy; loop strategy (snapshot vs dynamic); authority (client-predict vs server-only).


**PAT-BP-005 RepNotify Stability During Pickup (Don’t Clear Mid-Flow)**
- **Use when:** First pickup replicates fine, but second pickup leaves the client acting like the new weapon is `None`/unchanged (OnRep/equip/UI doesn’t update).
- **Schema:** Inputs: RepNotify `LootedWeapon` (weapon ref), pickup RPC(s), equip/attach logic, UI update path. Assumption: replication/OnRep timing is not guaranteed relative to RPC order and other state writes.
- **Steps:**
  1) **Remove** any `Set LootedWeapon (RepNotify) = None` from the **pickup/equip** code path.
  2) Keep `LootedWeapon` valid through: pickup → equip/attach → UI refresh.
  3) Move the “clear” to the **end of the drop** code path: after detach/physics/collision settle, then `Set LootedWeapon (RepNotify) = None`.
  4) If you need a “consumed” signal, use a separate non-RepNotify flag/event (or clear after the client confirms processing).
- **Checks:**
  - (1) Client successfully picks up weapon #1 and weapon #2 in the same session; OnRep fires and UI/equip reflects weapon #2.
  - (2) `LootedWeapon` never becomes `None` on client during pickup/equip unless explicitly dropping/clearing.
  - (3) In logs, the order is stable: set valid ref → OnRep processes → (later) clear on drop only.
- **Failure-modes:**
  - Still stale on client → value is being set/cleared in another place → search all `Set LootedWeapon` and centralize behind one setter.
  - OnRep doesn’t run for second pickup → ref is identical (same object) or not “changed” → ensure you assign the new actor ref (or use a separate replicated counter/ID).
  - Multiplayer authority mismatch → client writes are overwritten → ensure setter runs on server; client only reads/requests via RPC.
- **Knobs:**
  - Clear policy: never auto-clear ↔ clear on drop end ↔ clear after client-ack
  - Debug verbosity: none ↔ print OnRep order ↔ include role/netmode + timestamps
  - Rep signal: RepNotify only ↔ RepNotify + “PickupSequenceId” counter
  - Safety: delay clear by N frames ↔ immediate clear after drop finalize
- **Anti-pattern (avoid):** Clearing a RepNotify reference (`Set w/ Notify = None`) inside/near the pickup flow. This can arrive “late” and wipe the client’s state between pickups.


**PAT-BP-006 RepNotify Clear Race Guard (Delay vs Deterministic Clear)**
- **Use when:** `WeaponToDrop` is set correctly to a valid ref, but then “randomly” becomes `None` early because a delayed `Set w/Notify WeaponToDrop = None` fires before drop replication/OnRep/physics completes.
- **Schema:** Inputs: RepNotify `WeaponToDrop` (weapon ref), drop sequence (detach/physics/collision/inventory), OnRep handlers, any post-loop Delay that clears state. Assumption: drop completion is not instantaneous; timing differs by net conditions, movement, and physics.
- **Steps (quick fix):**
  1) Identify the delayed clear: `Delay` → `Set WeaponToDrop (RepNotify) = None`.
  2) Increase the post-loop delay enough that drop/equip/OnRep/physics settle before clearing.
  3) Add debug prints before set-valid, before clear, and inside OnRep to verify ordering.
- **Steps (best practice): replace Delay with deterministic clear**
  1) Introduce a **DropState** (e.g., `IsDropping` or enum) and only clear when state transitions to “DropComplete”.
  2) Define “DropComplete” as a concrete condition, e.g.:
     - detach finished AND
     - physics enabled AND
     - inventory updated AND
     - `DroppedWeapon` (in-world actor) is valid (or replicated) AND
     - (optional) owning client has processed OnRep for the drop
  3) Clear: `Set WeaponToDrop (RepNotify) = None` only after the condition is true.
- **Checks:**
  - (1) During sprint + drop, `WeaponToDrop` remains valid until the drop is finished (no early `None`).
  - (2) Owning client consistently processes the replicated valid ref before any clear (verified by prints/timestamps).
  - (3) With higher ping / packet loss simulation, behavior remains stable (no race regressions).
- **Failure-modes:**
  - Still clears early → there are multiple clears → search all `Set WeaponToDrop` and centralize in one setter.
  - Delay “fix” is inconsistent across machines → timing still nondeterministic → implement deterministic clear condition.
  - OnRep order confusing → add a replicated `DropSequenceId` counter so OnRep can ignore stale clears.
- **Knobs:**
  - Clear strategy: longer delay ↔ deterministic state-based clear
  - Debug: none ↔ prints (role/netmode/time) ↔ full sequence tracing
  - Robustness: no ID ↔ `DropSequenceId` counter
  - Condition strictness: minimal (DroppedWeapon valid) ↔ full (detach+physics+inventory+ack)
- **Anti-pattern (avoid):** Using a short Delay to clear a RepNotify reference when the completion of the underlying drop/replication pipeline is variable.


### Drills
- **DRL-BP-001 (10 min):** Build a small function with 3 checks + 2 “common troubles”.
- **DRL-BP-002 (15 min):** Debug a wrong-branch bug using prints + one breakpoint.

- **DRL-BP-003 (15 min):** Reproduce a “variable becomes None” overlap-loop bug, then fix with `IsValid(Array Element)` + `IsValid(Output)` gates; add 2 checks (20 attempts + “skipped invalid” logging).

- **DRL-BP-004 (15 min):** Instrument pickup/drop replication order (prints with role + time), reproduce “second pickup stale,” then fix by removing mid-pickup clear and moving the RepNotify clear to drop-end; verify with 10 back-to-back double-pickups.

- **DRL-BP-005 (15 min):** Reproduce “WeaponToDrop clears early” by adding a too-short delay, then fix it two ways: (A) tune delay until stable, (B) replace delay with a deterministic DropComplete condition; verify with 10 sprint+drop reps under a simulated high-ping setting.
