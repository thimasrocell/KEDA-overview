# Squaring Section

Spare parts and downtime monitoring for a three-line tile factory. Single-file app (`index.html`), no build step.

- Overview of production lines, with machines coloured by status, for this month, last month, any month or year, or the last 30 days up to all time
- Reports page: downtime, availability by line, spares and spend, month by month and year by year
- Downtime log with causes, spare parts used and mean time to repair
- Spare parts stock with minimum and reorder levels
- Serialized assets, repair pipeline (local and abroad) and purchase orders
- Undo and redo (Ctrl+Z, Ctrl+Shift+Z), and add, edit or remove machines, lines, parts, serial-numbered assets, downtime, purchase orders and repairs
- Cloud database (Supabase, free tier) and export to Excel, CSV or Google Sheets

## Run it

Open `index.html` in a browser, or publish it with GitHub Pages (Settings, Pages, branch `main`).
Data is saved in the browser. Sample data can be reset from the sidebar.

## Connect the free cloud database

1. Create a free project at supabase.com.
2. In the SQL Editor run the setup shown on the **Data & sync** page of the app.
3. Copy the Project URL and the anon public key (Project Settings, API) into the app and press **Save and connect**.

The URL and key are stored only in your browser, never in this repository. Anyone who has both can read and edit the data, so keep them private.
Use the same workspace name on every device that should share data. If two devices change data at once, the app shows a banner and lets you choose which version to keep.

## Google Sheets

- **Download Excel file**, then in Google Sheets use File, Import, Upload.
- **Send to Google Sheets** pushes every table into a sheet you own, through a small Apps Script that the app shows and lets you copy.

## Recent additions

- Machine codes are assigned from the line code and rank (SL-01, K2-01). Use the ▲/▼ buttons on the Machines page to reorder; codes renumber everywhere.
- Spare part quantities are kept per location (Main stores plus each line). Use Move to transfer between locations.
- The Downtime page has the same period controls as the Overview (this month, last month, month and year pickers, all time) and a button to delete the records in the current view.
- Data & sync: upload your company logo, or clear all sample records in one step (lines, machines and parts are kept).
