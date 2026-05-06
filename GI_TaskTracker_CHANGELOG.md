# GI Task Tracker — Changelog

**Firebase DB:** `https://gi-task-tracker-default-rtdb.firebaseio.com`  
**GitHub Pages:** `https://kyleharmer.github.io/gi-tracker`  
**Data storage:** Firebase Realtime Database (REST API, no SDK)  
**Firebase project:** `gi-task-tracker` (Google account: Kyle)

---

## v11.0 — 2026-05-06
**Logo corrections + mobile action sheet fix + clean rebuild**
- Header and report logo corrected to v2 (GII-LOGO-TRANSPARENT copy, mix-blend-mode: screen + opacity 0.85) — the version that renders correctly on the dark green header
- PWA icons (favicon, iOS home screen, Android) use v3 (AI-generated clean white rounded icon) — no blend mode needed
- Fixed mobile action sheet bug: tapping Edit or View Change Log did nothing — root cause was `closeActionSheet()` nulling `_asTaskId/_asBucket/_asTab` before the action functions could read them — fixed by capturing to local variables first
- `data-tab` attribute on each task row — action sheet sets correct `state.activeTab` before calling edit/history/delete
- Full clean rebuild from source JS files — eliminates accumulated patch drift
- Seed data (173 tasks) now correctly injected at build time

---

## v10.0 — 2026-05-06
**PWA icons + tab change history**
- GII logo in browser tabs (favicon), iPhone/iPad home screen, Android/Chrome home screen
- Web App Manifest embedded — "GI Tracker", green theme, standalone display
- `apple-mobile-web-app-capable` — full-screen on iOS when installed
- Icons at 180×192×512px
- Tab change history: every tab creation, deletion, rename logged with timestamp, who, action
- Tab history stored in Firebase, visible in Dashboard (last 20 events)

**Install:** iOS → Safari → Share → Add to Home Screen | Android → Chrome → ⋮ → Add to Home Screen | Desktop → install icon in address bar

---

## v9.0 — 2026-05-06
**Cross-platform font consistency**
- Full fallback stacks: `Barlow → Segoe UI → system-ui → sans-serif`
- Async Google Fonts loading — renders immediately with fallbacks
- `-webkit-font-smoothing: antialiased` globally — fixes Windows jagged rendering

---

## v8.0 — 2026-05-06
**Mobile interaction + versioning**
- Double-click task row on desktop → edit modal
- Tap task row on mobile → bottom action sheet (Edit / Change Log / Delete)
- Touch vs mouse auto-detected
- Version number in app header, `APP_VERSION` constant at top of JS

---

## v7.0 — 2026-05-06
**Logo, visual polish, report**
- GII icon mark in header (mix-blend-mode: screen, opacity 0.85)
- Header gradient lightened, logo 50px, title 21px
- Update banner bright green, completed button blue-tinted
- Print/Save PDF button bold blue, report header prints in color
- GII logo in PDF report, active tab preserved on remote update load

---

## v6.0 — 2026-05-06
**Firebase REST API — live shared sync**
- Pure `fetch()` — no SDK, no eval(), works on GitHub Pages/SharePoint/anywhere
- Real-time via Server-Sent Events, 15s polling fallback
- Data wrapped as `{d:"..."}` to avoid Firebase key restrictions
- User name prompt on first open, sync dot, update banner, Backup/Restore

---

## v5.0 — 2026-05-06
**Completed tasks + countdown badges + validation**
- Completed tasks hidden by default, toggle to reveal with count
- Countdown badge on tasks due within 14 days
- Input maxlength on all fields, auto-save debounced 800ms
- PDF report with configurable scope, charts, tables

---

## v4.0 — 2026-05-06
**Excel import — 8 PM tabs, 173 tasks**
- Kyle, Favs, Noah, Kendra, Software-Kendra, Service-Jonah, Jason, Design Bob & Cody
- Per-tab custom buckets, real task data, normalized dates/statuses

---

## v3.0 — 2026-05-06
**Owner/Supporting, My Tasks, exports, change log**
- Owner (green) + Supporting (blue) with autocomplete
- My Tasks view, priority flags, CSV export, per-task change log, column sort

---

## v2.0 — 2026-05-06
**Per-tab config + dashboard**
- Per-tab column/bucket configuration, Dashboard with stats + 3 charts + filterable table

---

## v1.0 — 2026-05-06
**Initial build — localStorage only**
- Single HTML file, 8 tabs, task fields, due date color coding

---

## Deployment reference

| Item | Value |
|------|-------|
| GitHub repo | kyleharmer/gi-tracker |
| Live URL | https://kyleharmer.github.io/gi-tracker |
| Upload as | index.html |
| Firebase project | gi-task-tracker |
| Firebase DB URL | https://gi-task-tracker-default-rtdb.firebaseio.com |
| Firebase rules | `{".read": true, ".write": true}` — internal only |
| API key | Embedded in HTML — internal use only |

**Moving hosting:** Data lives in Firebase. Move `index.html` anywhere — same credentials = same data.  
**Backup:** Header Backup button = full JSON download. Restore uploads it back for whole team.  
**Updating version:** Change `APP_VERSION` at top of JS, add entry here, upload both files.  
**Rule:** Every HTML release = also release updated CHANGELOG.md.
