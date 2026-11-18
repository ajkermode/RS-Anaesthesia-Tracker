# RS Anaesthesia Tracker

Personal planner for an 8-week consultant rota: week/fortnight focus view with copyable summary, month and year-at-a-glance views, leave booking by clinical session with quick wins and breaks, and a logbook of sessions by theatre or location.

Data is saved in the browser on each device (localStorage). To keep devices in step, turn on **Settings → Sync between devices**, which stores the data in a secret gist on your GitHub account (needs a classic token with the `gist` scope). **Settings → Backup** copies it manually.

Hosted with GitHub Pages (Settings → Pages → deploy from `main`).

## Rota sync (CLW)

`.github/workflows/rota.yml` runs `scripts/fetch_rota.py` five times a day. It reads the CLW work and leave calendars and saves a compact `rota.json` into the same secret gist the planner syncs with. The planner then shows theatre allocations, on-calls and rota leave. No rota data is stored in this repo.

Repository secrets needed (Settings → Secrets and variables → Actions): `CLW_WORK_URL`, `CLW_LEAVE_URL`, `GIST_TOKEN` (classic token with the `gist` scope) and `GIST_ID`.

## Logbook

The Logbook tab has DCC and SPA toggles. DCC counts sessions from the CLW work calendar by theatre or location, as collapsible groups with sessions and PAs (1 session = 1.25 PA). SPA lists Professional and Study Leave from the CLW leave calendar and lets you record CPD, teaching, audit and research activities, which are saved and synced with your other data. A Logbook Report button prints the DCC report, the SPA report or both for the displayed date range.

## Structure

`index.html` is the whole app (styles, data model and views in one file). `sw.js` keeps a copy for offline use and always fetches the newest version when online.
