# Hospital X — Healthcare Analytics Dashboard

An interactive, browser-based analytics dashboard for hospital patient data. Upload any Excel or CSV file with healthcare columns and instantly get filterable charts across demographics, trends, and costs — with **zero installation and zero backend**.

![Dashboard preview](https://raw.githubusercontent.com/DrFarooqAi/hospital-X-DataBoard/main/preview.png)

## Live Demo

**Open directly in your browser — no download needed:**
[https://drfarooqai.github.io/hospital-X-DataBoard/Dr_Farooq_Hospital_X_Dashboard.html](https://drfarooqai.github.io/hospital-X-DataBoard/Dr_Farooq_Hospital_X_Dashboard.html)

Or download [`Dr_Farooq_Hospital_X_Dashboard.html`](Dr_Farooq_Hospital_X_Dashboard.html) and open it locally.

## Features

- **Smart column detection** — automatically recognises common healthcare column names (patient name, age, gender, diagnosis, admission/discharge dates, billing, department, doctor, insurance, medications, etc.)
- **Three dashboard tabs**
  - **Demographics** — patient distribution by condition, admission type, age/gender breakdown, top medications, department heatmap
  - **Key Trends** — weekday vs. weekend admissions, length-of-stay distribution, monthly trends
  - **Treatment & Cost** — billing by admission type, LOS, condition, and insurance provider
- **Real-time filters** — slice by medical condition, year/month, department, and gender
- **KPI summary bar** — total patients, avg billing, avg length of stay, avg age, unique doctors, unique beds
- **100% private** — all data stays in your browser; nothing is uploaded anywhere

## How to Use

1. Download or clone this repository
2. Open `Dr_Farooq_Hospital_X_Dashboard.html` in Chrome, Firefox, Edge, or Safari
3. Click **Upload Data** and select an Excel (`.xlsx` / `.xls`) or CSV file
4. The dashboard auto-generates — use the sidebar filters and tabs to explore

A sample dataset (`synthetic_healthcare_data.xlsx`) is included so you can try it immediately.

## Accepted Column Names

The dashboard uses fuzzy matching — your columns don't need to match exactly. Recognised patterns include:

| Field | Example column names |
|---|---|
| Patient name | `Patient Name`, `Name`, `Full Name` |
| Age | `Age`, `Patient Age` |
| Gender | `Gender`, `Sex` |
| Diagnosis / Condition | `Medical Condition`, `Diagnosis`, `Condition` |
| Admission date | `Date of Admission`, `Admit Date`, `Admission Date` |
| Discharge date | `Discharge Date`, `Date of Discharge` |
| Billing | `Billing Amount`, `Bill`, `Charge`, `Cost` |
| Department | `Department`, `Ward`, `Unit` |
| Doctor | `Doctor`, `Physician`, `Provider` |
| Insurance | `Insurance Provider`, `Payer` |
| Medication | `Medication`, `Drug`, `Prescription` |
| Room / Bed | `Room Number`, `Bed`, `Room` |

Unrecognised columns are silently ignored; visualisations that depend on a missing field are hidden automatically.

## Tech Stack

| Library | Version | Purpose |
|---|---|---|
| [Chart.js](https://www.chartjs.org/) | 4.4.0 | All charts (loaded from CDN) |
| [SheetJS](https://sheetjs.com/) | 0.18.5 | Excel/CSV parsing (loaded from CDN) |
| Vanilla JS / CSS | — | Everything else |

No Node.js. No build step. No dependencies to install.

## Author

**Dr. Muhammad Farooq** — [github.com/DrFarooqAi](https://github.com/DrFarooqAi)

## License

MIT — free to use, modify, and share.
