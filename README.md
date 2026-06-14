# PIDC Workplan Maker

A browser-based tool for building field operations workplans for **Girls Tracking** and **Household (HH/GIRLS) interview** phases. Enter a start date and staffing targets — the app schedules working days, refresher training, and buffer periods while skipping weekly offs and Pakistan public holidays.

## Features

- **Three plan modes**
  - Full FOP — Tracking + HH/GIRLS (linked phases)
  - Tracking only — Girls tracking exercise
  - HH/GIRLS only — School girls, mothers, and fathers interviews

- **District presets** — D.I. Khan, Hangu, Lakki Marwat, Torghar, or Custom with editable parameters

- **Automatic scheduling** — Calculates daily targets, end dates, and milestones from:
  - Field staff count and per-day capacity
  - Refresher/training days at phase start
  - Buffer days at phase end (data validation)
  - Configurable weekly off days
  - Pakistan public holidays (Google Calendar)

- **Full FOP linking** — HH phase can start automatically the day after tracking buffer ends, or on a manually chosen date

- **Results & export**
  - Summary cards and milestone timeline
  - Searchable, filterable day-by-day schedule
  - Export to **CSV** or **DOC** (Word-compatible)
  - Print-friendly report layout

## Quick Start

No install or build step. Open the app in any modern browser:

1. Open `PIDC_Workplan_Maker.html` (double-click or serve locally).
2. Select a **district** and **plan type**.
3. Adjust targets, staff, refresher days, and buffer days as needed.
4. Set the **project start date** and **weekly off** days.
5. Click **Generate Workplan**.
6. Export or print from the results panel.

### Local server (optional)

Some browsers restrict API calls when opening files directly. If holiday fetching fails, serve the folder locally:

```bash
# Python 3
python -m http.server 8080

# Node.js (npx)
npx serve .
```

Then open `http://localhost:8080/PIDC_Workplan_Maker.html`.

## Configuration

### Google Calendar API

Public holidays are loaded from the official Pakistan holiday calendar via the Google Calendar API. The API key is set in `PIDC_Workplan_Maker.html` under `Config.API_KEY`.

If you see a calendar API error:

1. Create or use a Google Cloud project with the **Calendar API** enabled.
2. Create a browser-restricted API key.
3. Replace `Config.API_KEY` with your key.

### District presets

Preset districts live in the `Districts` object in the HTML file. Each preset includes default start dates, targets, staff counts, weekly offs, and buffer settings. Choose **Custom** to enter values manually.

## How scheduling works

| Day type | Behavior |
|----------|----------|
| **Refresher / Training** | Fixed days at the start of each phase |
| **Working** | Field activity with daily planned output based on staff × capacity |
| **Weekly off** | No field work; day skipped in target counting |
| **Public holiday** | Fetched from Google Calendar; no field work |
| **Buffer** | Fixed days at the end of tracking for data validation |

For **HH/GIRLS**, each working day plans interviews for school girls, mothers, and fathers (3× the school-girls target over the phase).

## Project structure

```
.
├── PIDC_Workplan_Maker.html   # Single-file app (HTML, CSS, JavaScript)
└── README.md
```

Everything runs client-side in one self-contained HTML file — no dependencies, frameworks, or backend.

## Browser support

Works in current versions of Chrome, Edge, Firefox, and Safari. Requires JavaScript and network access for holiday lookup.

## License

Not specified. Add a license file if you plan to share or open-source this repository.
