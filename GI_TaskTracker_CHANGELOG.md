# GI Task Tracker — Changelog

**Firebase DB:** `https://gi-task-tracker-default-rtdb.firebaseio.com`  
**Hosted:** GitHub Pages → `index.html`  
**Data storage:** Firebase Realtime Database (REST API, no SDK)

---

## v8.0 — 2026-05-06
**Mobile & UX improvements + versioning**
- Double-click any task row on desktop to open edit modal
- Tap any task row on mobile to open native-style action sheet (Edit / History / Delete)
- Touch vs mouse device automatically detected
- Version number (`v8.0`) now visible in app header
- Added this changelog

---

## v7.0
**Logo, visual polish**
- Replaced original banner logo with GII icon mark (PNG, mix-blend-mode: screen)
- Header gradient lightened so dark logo reads better
- Update banner changed to bright green — more prominent
- "Show/Hide Completed" button now blue-tinted, distinct from grey dropdowns
- Print/Save PDF button in report changed to bold blue
- Report header green prints correctly (`print-color-adjust: exact`)
- GII logo added to generated PDF report header

---

## v6.0
**Firebase REST API — live shared sync**
- Replaced Firebase JS SDK (caused eval() CSP block on GitHub Pages) with pure `fetch()` REST calls
- Real-time updates via Server-Sent Events (SSE) — no polling, instant push
- Falls back to 15-second polling if SSE unavailable
- User name prompt on first open (stored locally per browser)
- Sync status indicator in header (● Synced / Saving... / Offline)
- "Load updates" banner when another user saves
- Active tab preserved when loading remote updates
- Backup (JSON download) and Restore buttons in header
- Data wrapped as `{d: "..."}` to avoid Firebase key character restrictions (`/ . # $ [ ]`)

---

## v5.0
**Completed task hiding + countdown badges + validation**
- Completed tasks hidden by default on all tabs
- "Show/Hide Completed" toggle per tab
- Completed tasks shown greyed/struck-through with "Xd ago" label
- Active tasks due within 14 days show countdown badge ("3 days left")
- `completedAt` timestamp tracked when task marked complete
- Input `maxlength` on all form fields (textarea: 2000, text: 200, name: 120)
- Auto-save indicator ("Saving..." / "Saved by Kyle") in top-right corner

---

## v4.0 — Rev 4 (Excel import)
**All 8 PM tabs pre-loaded from Excel file**
- Kyle, Favs, Noah, Kendra, Software-Kendra, Service-Jonah, Jason, Design Bob & Cody
- Per-tab custom bucket structures matching original Excel layout
- 173 tasks seeded across all tabs
- Status values normalized across all sheets
- Excel serial dates converted to real dates

---

## v3.0 — Rev 3
**Owner/Supporting, My Tasks, export, change log**
- Split single "Responsible" field into Owner (green) + Supporting (blue)
- Folksonomy autocomplete on Owner/Supporting — learns names from entered data
- My Tasks view — type a name, see all their tasks across every PM tab
- My Tasks shows role (Owner vs Supporting) per task
- Priority flags: High / Medium / Low with color coding
- Export CSV per tab + Export All CSV from dashboard
- Change log per task — tracks what changed and when
- History modal (📋 icon) shows full change history
- Column sort by clicking any header

---

## v2.0 — Rev 2
**Per-tab configuration + global dashboard**
- Each PM tab has its own column and bucket config (inherits from global defaults)
- Toggle columns on/off per tab
- Add/remove/rename task buckets per tab
- Reset to global defaults option
- Global Dashboard tab with summary stats
- Charts: Tasks by PM (bar), Status Breakdown (donut), Due Date Health (stacked bar)
- Filterable master task table across all PMs (PM, bucket, status, priority, due date)
- Export All CSV from dashboard
- Generate Report button (PDF via print dialog)

---

## v1.0 — Rev 1
**Initial build**
- Single HTML file, no dependencies except Chart.js
- 8 PM tabs (from Excel structure)
- 6 default task buckets per tab
- Task fields: Customer, Details/Notes, Responsible, Status, Due Date, Next Milestone, Meeting Notes
- Due date color coding: Red (past due), Yellow (≤7 days), Green (on track)
- Stats row per tab (total, past due, due this week, complete)
- Search + status + priority filter bar
- Tab rename (in Configure panel)
- localStorage persistence
- Mobile responsive layout

---

## Deployment notes
- **GitHub repo:** rename file to `index.html` before uploading
- **Firebase rules:** `{".read": true, ".write": true}` — open (internal use only)
- **Moving hosting:** data lives in Firebase, not the HTML — move the file anywhere freely
- **Data migration:** use Backup (JSON) button → Restore on new instance
- **Firebase project:** `gi-task-tracker` (Google account: Kyle)
- **API key:** embedded in HTML — safe for internal SharePoint/GitHub access only
