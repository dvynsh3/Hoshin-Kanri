# Hoshin Kanri Live

A single-file, offline-friendly web tool for running a Hoshin Kanri X-Matrix session live. Edit the matrix on the page and every view updates instantly.

Built for the NPCI Bharat BillPay CEO review (H1 progress / H2 plan), where teams present and a Hoshin Kanri session follows.

## Quick start

1. Download or clone this repo.
2. Open `index.html` in Chrome or Edge (double-click works, no install or server needed).
3. Start building with the white **+** buttons in **Matrix → Full Matrix**, or load existing data with **Open File**.

An internet connection is needed on first use for the CDN libraries (SheetJS, ExcelJS, JSZip, html2canvas).

## Tabs

| Tab | What it shows |
|---|---|
| **Goals** | CEO goals as cards (3 per row) with linked objectives and Strong/Medium pills |
| **Overview** | Objectives → Initiatives → Metrics flow. Solid line = strong, dashed = medium. Click any block to highlight its connections |
| **Matrix** | Three toggles: Full Matrix (the X-matrix, the only editable surface), Objectives/Initiatives/Metrics, Goals/Objectives |
| **Initiative-Wise Details** | Per-initiative Sankey, Bow-tie and Tabulated views, plus a notes box that is included in exports |

## Editing (Matrix → Full Matrix)

- **Rename:** double-click any title. For initiatives, owners go in brackets, e.g. `Marketing (Amit, Kapil)`.
- **Delete:** rename to blank (removes the row or column and its links).
- **Links:** click a correlation cell to cycle None → Medium (2) → Strong (5) → None.
- **Add:** use the **+** buttons at the left (objective), right (metric), top (goal) and bottom (initiative).
- **Undo / Redo:** buttons above the matrix.

## Import and export

- **Open File** accepts:
  - `.xlsx` / `.xlsm`: one-time import from the Hoshin template workbook
  - `.zip`: an **Export all** bundle (restores your exact state, including notes)
  - `.json`: a raw `hoshin-state.json`
- **Export .xlsx** (Matrix tab): three sheets (Full Matrix, Objective/Initiatives/Metrics, Goals/Objectives).
- **Export .png**: current view only, black background, up to 3x resolution.
- **Export all** (top right): one zip with every PNG, the `.xlsx` and `hoshin-state.json`.

## Repo layout

```
index.html        The whole tool (HTML + CSS + JS in one file)
templates/        FULL Hoshin Kanri.xlsx, the Excel template that Open File can import
README.md
.gitignore
```

## Facilitation flow (summary)

1. Teams prepare up to 9 slides each (Overview & CEO Asks, H1 Scorecard, Partners & Categories, Growth, H1 Initiatives, Learnings, H2 Initiatives, Roadmap, Annexure), with Impact-Effort scoring done as homework.
2. Day 1: team presentations, with initiatives, objectives and metrics entered into the tool during Q&A.
3. Day 2: Hoshin session in the tool (lock objectives, confirm metrics and owners, build correlations, reconcile gaps, export).


## Browser notes

Chrome or Edge recommended. Data lives in the browser only, so use **Export all** to save your session.
