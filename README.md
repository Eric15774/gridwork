# Gridwork

A browser-based spreadsheet in a single HTML file. There's nothing to install and no account to make. Open the page, work on your sheets, and save them as JSON files you keep.

**Live app:** https://eric15774.github.io/gridwork/

## Features

- **Formulas:** about 100 functions, including `SUM`, `IF`, `VLOOKUP`, `XLOOKUP`, `SUMIFS`, `COUNTIFS`, `INDEX`/`MATCH`, text, date, trig, and finance functions (`PMT`, `FV`, `PV`)
- **Multiple sheets** in one file, with cross-sheet references like `=Budget!B11` or `='Lab data'!C4`
- **Fill handle:** drag the corner of a selection to copy formulas, or double-click it to fill down. Number series, dates, and text like "Week 1" count up
- **Rows and columns:** insert and delete from the right-click menu, and formulas adjust automatically
- **Charts:** line, bar, points, and pie. Two series can use independent left and right y axes over a shared x axis
- **Formatting:** number formats (currency, percent, dates), bold, italic, text and fill colors, borders, wrap text, and merge and center
- **Conditional formatting:** rules like "negative numbers in red" or "highlight values over 100"
- **Sort, find and replace, freeze panes, and cell notes**
- **Undo and redo** for every change
- **Files:** save and open Gridwork JSON, open and export Excel `.xlsx`, export CSV, and print

## Getting started

1. Open the live app, or download `index.html` and open it in any modern browser.
2. Type in a cell. Start a formula with `=`.
3. Click **Save JSON** (or press Ctrl+S) to keep a copy of your work.
4. Click **Open** to load a saved JSON, CSV, or Excel file.

**Help > Open the examples** loads a sample budget and a physics lab sheet that has a two-axis chart.

## Saving your work

Gridwork autosaves in your browser, but that copy stays on one computer and can be cleared with your browser data. Save JSON files for anything you want to keep.

- Keep your JSON files in a cloud folder such as Google Drive, OneDrive, or Dropbox. That way they're backed up and you can reach them from any computer.
- **Don't commit personal spreadsheets to this repository.** It's public, so anyone can read files stored here.

## Keyboard shortcuts

| Keys | Action |
|---|---|
| Enter or F2 | Edit cell |
| Ctrl+Z / Ctrl+Y | Undo / redo |
| Ctrl+C / Ctrl+X / Ctrl+V | Copy / cut / paste |
| Ctrl+D / Ctrl+R | Fill down / fill right |
| Ctrl+B / Ctrl+I | Bold / italic |
| Ctrl+F / Ctrl+H | Find / find and replace |
| Ctrl+Arrow | Jump to the edge of the data |
| Shift+Arrow | Extend the selection |
| Shift+F2 | Add or edit a note |
| Ctrl+PageUp / Ctrl+PageDown | Switch sheets |
| Ctrl+S / Ctrl+O / Ctrl+P | Save JSON / open / print |

## File format

Saved files are plain JSON:

```json
{
  "app": "Gridwork",
  "version": 2,
  "name": "Monthly budget",
  "sheets": [
    {
      "name": "Budget",
      "cells": {
        "A1": { "v": "Groceries" },
        "B1": { "v": "650", "f": "cur" },
        "B2": { "v": "=SUM(B1:B1)", "b": true }
      }
    }
  ]
}
```

Each cell stores its raw entry in `v` (a value or a formula starting with `=`). Formatting is stored in short keys: `f` (number format), `b` (bold), `i` (italic), `a` (alignment), `fc` and `bg` (colors), `bd` (borders), `w` (wrap), and `n` (note). Each sheet also stores its column widths, frozen panes, merges, conditional formats, and charts.

## Limitations

- Excel export keeps values, formulas, number formats, merges, column widths, and notes. Colors, borders, conditional formatting, and charts are not exported.
- Each sheet holds up to 2,000 rows and 104 columns.
- An internet connection is needed for charts and for Excel import and export, which load these libraries from the jsDelivr CDN:
  - [Chart.js](https://www.chartjs.org/) 4.4.1
  - [SheetJS](https://sheetjs.com/) 0.18.5
- To reference another sheet in a formula, type its name (for example `=Lab!C4`). Clicking a cell on another tab while editing a formula doesn't insert the reference.

## Deploying

The app is a single static file, so it runs on GitHub Pages as is. In the repository's **Settings > Pages**, set the source to the `main` branch, root folder. To update the app, replace `index.html` and commit.
