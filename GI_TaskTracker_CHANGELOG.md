# GI Task Tracker — Changelog

**Firebase DB:** `https://gi-task-tracker-default-rtdb.firebaseio.com`  
**GitHub Pages:** `https://kyleharmer.github.io/gi-tracker`  
**Data storage:** Firebase Realtime Database (REST API, no SDK)  
**Firebase project:** `gi-task-tracker` (Google account: Kyle)

---

## v9.0 — 2026-05-06
**Cross-platform font consistency**
- Added full font fallback stacks everywhere: `Barlow → Segoe UI → system-ui → sans-serif` and `Barlow Condensed → Segoe UI Semibold → Segoe UI → system-ui → sans-serif`
- Segoe UI fallback ensures clean rendering on Windows 10/11 even if Google Fonts CDN is blocked or times out
- Google Fonts now loads asynchronously (non-blocking) — page renders immediately with fallback fonts rather than waiting on CDN
- Added `-webkit-font-smoothing: antialiased` and `text-rendering: optimizeLegibility` globally — fixes jagged/sharp edge rendering on Windows browsers
- Applied smoothing to all 19 font references across CSS

---

## v8.0 — 2026-05-06
**Mobile interaction + versioning**
- Double-click any task row on desktop opens edit modal directly
- Single tap any task row on mobile opens native-style bottom action sheet (Edit / View Change Log / Delete) with large touch targets
- Touch vs mouse device automatically detected (`ontouchstart` / `maxTouchPoints`)
- Subtle "double-click to edit" hint text appears on desktop row hover
- Version number (`v8.0`) now visible in app header next to "Task Tracker"
- `APP_VERSION` and `BUILD_DATE` constants at top of JS for easy future updates
- Added changelog document (`GI_TaskTracker_CHANGELOG.md`)

---

## v7.0 — 2026-05-06
**Logo, visual polish, report improvements**
- Replaced original banner logo with GII icon mark (PNG, `mix-blend-mode: screen`, `opacity: 0.85`)
- Header gradient lightened so dark GII mark reads better against background
- Logo height increased to 50px, "Task Tracker" title increased to 21px
- Update banner changed to bright green (#4a9a20) — more prominent against header
- "Show/Hide Completed" button now blue-tinted, label reads "Show/Hide Completed (N)" — distinct from grey dropdowns
- Print/Save PDF button in report changed to bold blue with drop shadow
- Report header green prints correctly (print-color-adjust: exact added globally)
- GII logo added to generated PDF report header
- Active tab preserved when loading remote updates (no longer jumps to last-saved tab)

---

## v6.0 — 2026-05-06
**Firebase REST API — live shared sync (no SDK)**
- Replaced Firebase JS SDK (caused eval() CSP block on GitHub Pages) with pure fetch() REST calls
- Works on GitHub Pages, SharePoint, file://, anywhere — no CSP issues
- Real-time updates via Server-Sent Events (SSE) — instant push when another user saves
- Falls back to 15-second polling if SSE unavailable
- Data wrapped as {d: "..."} to avoid Firebase key character restrictions (/ . # $ [ ])
- User name prompt on first open per browser (stored in localStorage only)
- Sync status dot in header: green = synced, yellow = saving, red = offline
- "Load updates" banner when another user saves
- Backup (JSON download) and Restore buttons in header

---

## v5.0 — 2026-05-06
**Completed task handling + countdown badges + input validation**
- Completed tasks hidden by default on all tabs
- "Show/Hide Completed" toggle per tab shows count
- Revealed completed tasks greyed/struck-through with "Xd ago" label
- completedAt timestamp tracked per task
- Active tasks due within 14 days show live countdown badge ("3 days left" etc.)
- Input maxlength enforced: textarea 2000, text 200, name/owner 120, tab name 60
- Auto-save debounced 800ms — "Saving..." / "Saved by [Name]" indicator
- Report generation: configurable PDF via browser print dialog
- Report includes summary stats, 3 charts, task tables by PM/bucket
- Report config saved as defaults per user

---

## v4.0 — 2026-05-06
**Full Excel import — all 8 PM tabs pre-loaded**
- Kyle, Favs, Noah, Kendra, Software-Kendra, Service-Jonah, Jason, Design Bob & Cody
- Per-tab custom bucket structures matching original Excel layout
- 173 tasks seeded with real data from Excel file
- Excel serial dates converted to proper dates
- Status values normalized across all sheets

---

## v3.0 — 2026-05-06
**Owner/Supporting split, My Tasks, exports, change log**
- Split "Responsible" into Owner (green) + Supporting (blue) with autocomplete
- Folksonomy autocomplete learns all names entered across all tabs
- My Tasks view — search any name across all PM tabs, shows role and context
- Priority flags: High / Medium / Low with color-coded badges
- Export CSV per tab + Export All CSV from Dashboard
- Per-task change log with history modal
- Column sort by clicking any header

---

## v2.0 — 2026-05-06
**Per-tab configuration + global dashboard**
- Per-tab column and bucket configuration (inherits global defaults)
- Toggle/add/remove columns and buckets per tab
- Global Dashboard: summary stats, 3 charts, filterable master task table
- Export All CSV from Dashboard
- Tab rename in Configure panel
- Mobile responsive layout

---

## v1.0 — 2026-05-06
**Initial build — localStorage only**
- Single self-contained HTML file
- 8 PM tabs, 6 default buckets per tab
- Task fields: Customer, Details/Notes, Responsible, Status, Due Date, Milestone, Meeting Notes
- Due date color coding (red/yellow/green)
- Stats row, search + filter bar per tab
- localStorage persistence (per browser, not shared)

---

## Deployment reference

| Item | Value |
|------|-------|
| GitHub repo | kyleharmer/gi-tracker |
| Live URL | https://kyleharmer.github.io/gi-tracker |
| File to upload | Rename to index.html before uploading |
| Firebase project | gi-task-tracker |
| Firebase DB URL | https://gi-task-tracker-default-rtdb.firebaseio.com |
| Firebase rules | {".read": true, ".write": true} — open (internal only) |
| API key | Embedded in HTML — safe for internal use only |

**Moving hosting:** Data lives in Firebase, not the HTML. Move index.html anywhere freely — same credentials = same data.

**Backup:** Use the Backup button in the header to download a full JSON snapshot. Restore button uploads it back to Firebase for the whole team.

**Updating version:** Change APP_VERSION at the top of the JS and add an entry here before uploading.
