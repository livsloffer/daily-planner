# Olivia’s Daily Planner

A static website: assignment tracker, travel logistics with a world map, and a 7‑day Google Calendar view.

- **Assignments and travel** load from `data/assignments.csv` and `data/travel.csv` the first time you open the site in a browser. After that, your edits (checkboxes, points, new items, countries) are saved in that browser's local storage.
- **Reset from CSV** (on each page) reloads that section from its CSV, replacing edits made in the browser.
- **Download CSV** saves the current data in the same layout as the CSVs. Commit it back to `data/` to share your edits across devices.

## Hosting on GitHub Pages

Settings → Pages → Build and deployment → Source: *Deploy from a branch*, Branch: `main`, folder `/ (root)`. The site appears at `https://livsloffer.github.io/daily-planner/`.

> The site and everything in this repo, including the CSVs, is readable by anyone with the link.

## Connecting Google Calendar

The calendar card calls the Google Calendar API from the browser, signed in with your Google account (read‑only access). It needs an OAuth Client ID:

1. Go to <https://console.cloud.google.com/>, create a project (e.g. *Daily Planner*).
2. **APIs & Services → Library**: enable **Google Calendar API**.
3. **APIs & Services → OAuth consent screen** (Google Auth Platform): user type **External**, fill in the app name and your email. Under **Audience**, add your Google account as a **test user**. Under **Data access**, add the scope `.../auth/calendar.readonly`.
4. **APIs & Services → Credentials → Create credentials → OAuth client ID**: type **Web application**. Under **Authorized JavaScript origins** add:
   - `https://livsloffer.github.io`
   - `http://localhost:8000` (for testing on your computer)
5. Copy the Client ID (ends in `.apps.googleusercontent.com`) into `config.js` as `googleClientId`, then commit and push.

Open the site and press **Connect Google Calendar**. Google sign‑in lasts about an hour per tab; after that the card shows a **Reconnect** button.

## Running locally

Browsers block the CSV and map files when `index.html` is opened directly from disk, so serve the folder:

```
python3 -m http.server 8000
```

Then open <http://localhost:8000>.
