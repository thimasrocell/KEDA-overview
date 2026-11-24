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
- Parts can have serial numbers for some units and not others. Repairs can be raised for a serial-numbered unit or for plain stock quantity, and stock follows the item out and back.
- Each part records how many units are currently installed on each line (serial-numbered units fitted to machines are counted automatically).

## Deploy on Vercel

This is a single static page with no build step, so it deploys as is.

1. Sign in at vercel.com with GitHub and choose **Add New → Project**.
2. Import `KEDA-overview`. Leave Framework Preset as **Other**, leave Build Command and Output Directory empty (`vercel.json` already sets this), then **Deploy**.
3. Open the URL Vercel gives you, go to **Data & sync**, and enter your Supabase URL and anon key. They are stored in each browser, not in the code, so enter them once on every device or browser you use.

To avoid entering the keys on every device or browser, use either of these (after connecting once, both are on the **Data & sync** page):

- **Copy setup link**: open that link once in any browser and it connects by itself.
- **Copy config.js**: paste the text into `config.js` in this repo and commit it. Every visitor then connects automatically. Only do this if the repo is private or you are happy for anyone who can see it to be able to edit your data.

Every push to `main` redeploys automatically. The app works the same on GitHub Pages and Vercel, since all data lives in Supabase and the browser.
- **Spare costs:** import the monthly factory consumption or misc issue report (.xlsx). Only rows for your departments are kept, listed for you to assign to a machine, a whole line, or remove. Lines left unassigned for 60 days count against the line automatically. Alerts flag high value, repeated, missing-MRN, return and price-mismatch lines.
- **Testing take-outs:** a spare can be taken out for testing and returned unused. The part shows "Tested N× and returned" until it is issued to a machine; then the marker clears and the history ("used after N test take-outs") is kept.
- **Shifts:** set your shifts under Data & sync. Downtime can be logged by exact time (the shift is worked out, and stops that cross a shift change are split) or by shift and total minutes. Downtime and Reports show downtime by shift.
- **Paste shift reports:** on the Downtime page, paste chat text and the app reads machine codes with time ranges or minutes (no AI, nothing leaves the browser, the pasted text is not saved). Review and import the rows you tick.

## Line performance (shift reports)
Paste the production message posted after each shift (e.g. "Keda 02 - 1643 sqm", yields, "Stoppages - (...)"). It runs in the browser only, without AI. Stoppages are sorted into Breakdown, Power or utility, Changeover and Break or sample. Availability = run time / scheduled shift time; "excluding changeovers" removes changeover time from the scheduled time. These are kept separate from machine downtime events.
