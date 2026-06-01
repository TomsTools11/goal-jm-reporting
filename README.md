# Jones-McDonald — Client Reporting

A simple static landing page that delivers account-review reports to
Jones-McDonald Insurance Agency, prepared by **GOAL Performance Marketing**.

The landing page (`index.html`) lists every report as a card showing its
title and the date it was created. Each card opens the full report, and every
report has an **"All reports"** button in the top-left that returns to the
landing page.

## Structure

```
.
├── index.html                              # Landing page (the reports list)
├── reports/
│   └── 2026-06-01-performance-review.html  # A self-contained report
├── assets/
│   └── goal-logo-white.png                 # GOAL logo (used on the landing page)
├── vercel.json                             # Vercel static-site config
└── README.md
```

Reports are fully self-contained HTML files (styles and the logo are embedded),
so they also open correctly on their own.

## Adding a new report

1. Drop the new report's HTML file in `reports/`, using a
   `YYYY-MM-DD-short-title.html` name so reports sort by date, e.g.
   `reports/2026-09-01-q3-review.html`.

2. Add the **"All reports"** back button to the new report. The reports use a
   dark sidebar (`<aside class="side">`), so add this as the sidebar's first
   child (it inherits the `.backbtn` styles already in those reports):

   ```html
   <a class="backbtn" href="../index.html">
     <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"
          stroke-linecap="round" stroke-linejoin="round">
       <line x1="19" y1="12" x2="5" y2="12"></line>
       <polyline points="12 19 5 12 12 5"></polyline>
     </svg>All reports
   </a>
   ```

3. Add a card for it in `index.html`, inside `<main class="cards">`. Newest
   reports go first:

   ```html
   <a class="card" href="reports/2026-09-01-q3-review.html">
     <span class="tag">Performance Review</span>
     <h3>Q3 Performance Review</h3>
     <div class="date">
       <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
            stroke-linecap="round" stroke-linejoin="round">
         <rect x="3" y="4" width="18" height="18" rx="2"></rect>
         <line x1="16" y1="2" x2="16" y2="6"></line>
         <line x1="8" y1="2" x2="8" y2="6"></line>
         <line x1="3" y1="10" x2="21" y2="10"></line>
       </svg>
       September 1, 2026
     </div>
     <span class="cta">View report <span class="ar">&rarr;</span></span>
   </a>
   ```

## Deploying on Vercel

This is a zero-build static site, deployed straight from GitHub:

1. In Vercel, **Add New → Project** and import this repository.
2. Framework Preset: **Other** (no build command, no output directory).
3. Deploy. Every push to the production branch redeploys automatically.

`vercel.json` enables `cleanUrls`, so reports are served at extension-less URLs
(e.g. `/reports/2026-06-01-performance-review`).

## Previewing locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```
