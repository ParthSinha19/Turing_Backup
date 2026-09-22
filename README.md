# AI Club Session Dashboard

A small static dashboard for reviewing Turing Education AI Club session
feedback (from the Google Form export). Blue-and-white theme, no server —
everything runs in the browser and reads `feedback.csv`.

## Files

- `index.html` — the dashboard (structure, styling, and the logic below)
- `feedback.csv` — the session feedback data (replace this with a fresh
  export from Google Forms/Sheets whenever you have new responses — same
  column headers, just more rows)

## What it does

- **Groups schools by keyword**, so inconsistent spellings from the form
  (e.g. "Brighton Prep", "Brighton College Prep", "Brighton school") are
  shown as one school. This is the `SCHOOL_ALIASES` list near the top of
  the `<script>` in `index.html` — add a new `{ keywords: [...], canonical: "..." }`
  entry whenever a new school or spelling shows up.
- **Grades each session as Major / Minor / No issue** from the worded and
  categorical answers (safeguarding notes, technical problems, priority
  score, behavioural notes, follow-up requests). Major issues are flagged
  red and sit at the top of attention; minor ones are amber. The exact
  rules are documented and easy to tweak in the `gradeIssue()` function.
- **Drops the submission timestamp** — only the date of the session is
  shown, as requested.
- **Resolve / reopen** — admins can mark an issue resolved from the card;
  this is remembered in that browser's local storage (see note below).

## Hosting on GitHub Pages

1. Create a new GitHub repository (public, or private with GitHub Pages
   enabled on your plan).
2. Add `index.html` and `feedback.csv` to the repository root (or to a
   `/docs` folder — just keep them in the same folder as each other).
3. In the repo, go to **Settings → Pages**, and under "Build and
   deployment" set the source branch (e.g. `main`) and folder (`/root` or
   `/docs`, matching step 2).
4. GitHub will publish it at `https://<your-username>.github.io/<repo-name>/`
   within a minute or two.
5. To update the data later, just replace `feedback.csv` with a new export
   and push — no code changes needed unless a brand-new school name needs
   an alias added.

## A note on "resolved" status

Because this is a static site with no database, marking an issue resolved
is saved in **that browser's local storage only** — it won't sync between
devices or show the same for every admin who opens the page. If several
people need to see the same resolved/open state, the next step would be a
small shared backend (e.g. a Google Sheet written back to via Apps Script,
or a tiny database) — happy to help set that up if it becomes useful.
