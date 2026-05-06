# GI Task Tracker — Changelog

**Firebase DB:** `https://gi-task-tracker-default-rtdb.firebaseio.com`  
**GitHub Pages:** `https://kyleharmer.github.io/gi-tracker`  
**Data storage:** Firebase Realtime Database (REST API, no SDK)  
**Firebase project:** `gi-task-tracker` (Google account: Kyle)

---

## v11.0 — 2026-05-06
**New logo + mobile action sheet fix**
- Replaced GII dark-background logo with new AI-generated app icon (white/rounded background, clean PNG — no blend mode hack required)
- New logo used everywhere: header, browser tab favicon, iOS/Android home screen icon, PWA manifest, and PDF report header
- PWA icons regenerated at 180×192×512px from new logo
- Fixed mobile action sheet bug: tapping Edit or View Change Log did nothing — root cause was `closeActionSheet()` nulling `_asTaskId` and `_asBucket` before the action functions could read them. Fixed by capturing values to local variables before closing
- Added `data-tab` attribute to each task row — action sheet now explicitly sets `state.activeTab` to the correct tab before calling edit/history/delete, preventing wrong-tab lookup errors
- Full clean rebuild from source JS files — eliminates accumulated patch debt

---

## v10.0 — 2026-05-06
**PWA icons + tab change history**
- GII logo appears in browser tabs (favicon), iPhone/iPad home screen, and Android/Chrome home screen
- Web App Manifest embedded — app name "GI Tracker", GI green theme color, standalone display mode
- `apple-mobile-web-app-capable` — opens full-screen on iOS with no browser chrome when installed
- Icons generated at 180×192×512px
- Tab change history tracked: every tab creation, deletion, and rename logged with timestamp, action, tab name, and who did it
- Tab history stored in Firebase with all other state
- Last 20 tab events visible at bottom of Dashboard in "Tab Change History" table
- Stores up to 100 events total, oldest trimmed automatically

**To install on iPhone/iPad:** Open URL in Safari → Share → "Add to Home Screen" → Add
**To install on Android:** Open in Chrome → three-dot menu → "Add to Home Screen"
**To install on desktop:** Click the install icon in the address bar (Chrome/Edge)

---

## v9.0 — 2026-05-06
**Cross-platform font consistency**
- Full font fallback stacks: `Barlow → Segoe UI → system-ui → sans-serif` and `Barlow Condensed → Segoe UI Semibold → Segoe UI → system-ui → sans-serif`
- Segoe UI fallback ensures clean rendering on Windows 10/11 if Google Fonts CDN is blocked
- Google Fonts loads asynchronously (non-blocking) — page renders immediately
- Added `-webkit-font-smoothing: antialiased` and `text-rendering: optimizeLegibility` globally
- Fixes jagged/sharp edge rendering on Windows browsers

---

## v8.0 — 2026-05-06
**Mobile interaction + versioning**
- Double-click any task row on desktop opens edit modal
- Single tap any task row on mobile opens native-style bottom action sheet (Edit / View Change Log / Delete)
- Touch vs mouse device automatically detected
- Subtle "double-click to edit" hint on desktop row hover
- Version number visible in app header (v8.0+)
- `APP_VERSION` and `BUILD_DATE` constants at top of JS

---

## v7.0 — 2026-05-06
**Logo, visual polish, report improvements**
- GII icon mark in header (mix-blend-mode: screen)
- Header gradient lightened, logo 50px, title 21px
- Update banner bright green — more prominent
- "Show/Hide Completed" button blue-tinted, distinct from dropdowns
- Print/Save PDF button bold blue with drop shadow
- Report header prints in color (print-color-adjust: exact)
- GII logo in PDF report header
- Active tab preserved when loading remote updates

---

## v6.0 — 2026-05-06
**Firebase REST API — live shared sync**
- Pure `fetch()` REST calls — no SDK, no eval(), works on GitHub Pages
- Real-time updates via Server-Sent Events (SSE)
- Falls back to 15-second polling if SSE unavailable
- Data wrapped as `{d: "..."}` to avoid Firebase key restrictions
- User name prompt on first open per browser
- Sync status dot: green = synced, yellow = saving, red = offline
- "Load updates" banner when another user saves
- Backup and Restore buttons in header

---

## v5.0 — 2026-05-06
**Completed tasks + countdown badges + validation**
- Completed tasks hidden by default, toggle to reveal
- Revealed completed tasks greyed/struck-through with "Xd ago"
- Active tasks due within 14 days show countdown badge
- Input maxlength enforced on all fields
- Auto-save debounced 800ms with save indicator
- PDF report generation (configurable scope, charts, tables)

---

## v4.0 — 2026-05-06
**Excel import — 8 PM tabs, 173 tasks**
- Kyle, Favs, Noah, Kendra, Software-Kendra, Service-Jonah, Jason, Design Bob & Cody
- Per-tab custom buckets matching Excel layout
- Real task data, normalized dates and statuses

---

## v3.0 — 2026-05-06
**Owner/Supporting, My Tasks, exports, change log**
- Owner (green) + Supporting (blue) with autocomplete
- My Tasks view across all tabs
- Priority flags, CSV export, per-task change log, column sort

---

## v2.0 — 2026-05-06
**Per-tab config + dashboard**
- Per-tab column/bucket configuration
- Dashboard: stats, 3 charts, filterable master table

---

## v1.0 — 2026-05-06
**Initial build — localStorage only**
- Single HTML file, 8 tabs, task fields, due date color coding, localStorage

---

## Deployment reference

| Item | Value |
|------|-------|
| GitHub repo | kyleharmer/gi-tracker |
| Live URL | https://kyleharmer.github.io/gi-tracker |
| Upload as | index.html |
| Firebase project | gi-task-tracker |
| Firebase DB URL | https://gi-task-tracker-default-rtdb.firebaseio.com |
| Firebase rules | `{".read": true, ".write": true}` |
| API key | Embedded in HTML — internal use only |

**Moving hosting:** Data lives in Firebase. Move `index.html` anywhere — same credentials = same data.  
**Backup:** Header Backup button downloads full JSON. Restore uploads it back for the whole team.  
**Updating version:** Change `APP_VERSION` at top of JS, add entry here, upload both files to GitHub.
