# GI Task Tracker — Changelog

---

## v11.2 — 2025-05-07
**Real-time Merge (Conflict-Safe Sync)**

Replaced the previous "last writer wins" update behavior with a full field-level merge system. Clicking "Load updates" no longer overwrites local changes — all work on all devices is preserved.

### What changed
- **`mergeStates()`** — new function that merges remote state into local state using per-task, per-field logic
- **`acceptUpdate()`** — now calls `mergeStates()` instead of `applyRemoteState()` (overwrite)
- **Task row render** — tasks with unresolved conflicts show a yellow **⚠** badge next to the customer name; hovering shows which fields were merged
- **CSS** — added `.conflict-row` (subtle yellow background) and `.conflict-badge` styles
- **`saveTask()`** — clears the conflict flag and badge when a user opens and saves a flagged task

### Merge rules
| Scenario | Behavior |
|---|---|
| Task added on PC1 only | Pulled into PC2 on merge |
| Task added on PC2 only | Kept — not overwritten by remote |
| Same task edited on both | Field-by-field merge: most-recent changelog timestamp wins per field |
| Task deleted remotely, exists locally | Restored with ⚠ conflict flag — deletion does not win |
| Task deleted locally, not in remote | Stays deleted — local intent respected |

### Changelog entries added on conflict
Merged tasks get a system changelog entry: `⚠ Merge: remote update applied to [fields]` or `⚠ Conflict: this task was deleted remotely but has been restored.`

---

## v11.1 — 2025-05-07
**Firebase Connection Fix**

Fixed a regression introduced in the v11 rebuild where the app showed "Check Firebase rules" on load even with correct open rules.

### Root cause
Three pieces of the Firebase REST layer were accidentally dropped during the v11 rebuild from source files:

1. **`fbRead()`** — lost the `{d: "..."}` unwrap logic. Raw wrapped object was returned directly, making `remote.tabs` undefined, causing the app to think the DB was empty.
2. **`fbWrite()`** — lost the `{d: JSON.stringify(data)}` wrap logic. Raw state was written directly, causing Firebase to reject keys containing spaces and slashes.
3. **SSE `put` handler** — checked `msg.data.tabs` before unwrapping, so every stream event was silently dropped.

### Fix
Restored all three patterns to match the confirmed-working v10 implementation. No other code was changed.

---

## v11.0 — Initial rebuild
Full rebuild from modular source files (`gi_firebase_rest.js` + `gi_main_v4c.js`). See handoff document for full feature list.

---

## v10.0 — Last stable pre-rebuild
Working reference version. Firebase REST layer confirmed functional. Used as diff baseline for v11.1 fix.
