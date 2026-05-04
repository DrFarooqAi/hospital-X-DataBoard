# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Summary

A single-file, client-side healthcare analytics dashboard. The **entire application lives in one HTML file**: [Dr_Farooq_Hospital_X_Dashboard.html](Dr_Farooq_Hospital_X_Dashboard.html). There is no build system, no package manager, no backend, and no framework — only vanilla JS, inline CSS, and CDN-loaded libraries.

## Running the App

Open `Dr_Farooq_Hospital_X_Dashboard.html` directly in a browser. No server, no install step. Upload `synthetic_healthcare_data.xlsx` (included) to test the full dashboard flow.

## External Dependencies (CDN only)

- **Chart.js 4.4.0** — all chart rendering
- **SheetJS (XLSX 0.18.5)** — Excel/CSV parsing
- **Google Fonts** — Inter, Space Grotesk, Space Mono

## Architecture

All code is in a single HTML file, structured as:

1. `<head>` — Google Fonts imports + all CSS styles (cyberpunk/neon aesthetic)
2. `<body>` — Static HTML shell (sidebar, KPI cards, tab containers)
3. `<script>` (bottom of body) — all application logic

### Data Flow

```
File upload → handleFile() → XLSX parse → RAW_DATA[]
  → detectSchema()  (maps raw column names → SCHEMA object)
  → enrichData()    (adds __admit, __disch, __los, __billing, __age)
  → buildFilters()  (populates filter dropdowns)
  → applyFilters()  → FILTERED_DATA[]
  → renderAll()     → renderKPIs() + renderDemographics() + renderTrends() + renderCost()
```

### Key Global State

| Variable | Purpose |
|---|---|
| `RAW_DATA` | All parsed rows from the uploaded file |
| `FILTERED_DATA` | Subset after active filters applied |
| `SCHEMA` | Maps semantic field names (e.g. `age`, `billing`) to actual column names |
| `CHART_INSTANCES` | Registry of active Chart.js instances (destroyed before re-render) |

### Schema Detection

`detectSchema(headers)` uses `FIELD_PATTERNS` — a map of semantic field → regex array — to fuzzy-match uploaded column headers. Unrecognised columns are silently skipped; visualisations that depend on a missing field are hidden automatically.

### Chart Helpers

All charts are drawn through thin wrappers that destroy any existing Chart.js instance on the same canvas before creating a new one:

`drawBar()` · `drawDonut()` · `drawHorizontalBar()` · `drawGroupedBar()` · `drawLine()`

### Tabs

| Tab | Render function | Content |
|---|---|---|
| Demographics | `renderDemographics()` | Condition distribution, admission types, age/gender, medications, dept heatmap |
| Key Trends | `renderTrends()` | Weekday vs weekend, LOS buckets, monthly trends |
| Treatment & Cost | `renderCost()` | Billing by admission type, LOS, condition, insurance |

## Editing Guidelines

- Edit the single HTML file directly — styles in `<style>`, logic in the bottom `<script>`.
- All filter changes call `applyFilters()` then `renderAll()` — follow this pattern for any new interactive control.
- When adding a new chart: add a `<canvas>` in the HTML, add a `drawXxx()` call in the appropriate `renderXxx()` function, and store the instance in `CHART_INSTANCES`.
- When adding a new detected field: add entries to `FIELD_PATTERNS` and handle the new `SCHEMA` key in `enrichData()` or the relevant render function.
- The `synthetic_healthcare_data.xlsx` file is the canonical test fixture; verify any schema-detection changes against it.
