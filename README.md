# Acuity Sourcing — Website

Static HTML site for acuitysourcing.com, deployed on Vercel.

## Structure

```
acuity-site/
├── index.html                             Home page
├── about.html                             About / origin story
├── work.html                              Selected work (portfolio, 7 cases)
├── how-i-work.html                        Services / engagement models
├── writing/
│   └── software-expensive.html            Flagship essay (first in series)
├── vercel.json                            Clean URLs config
└── README.md
```

## Deployment

Vercel auto-deploys from this repo. Any commit pushed to `main` triggers a redeploy.

Clean URLs are enabled via `vercel.json`, so `/about` serves `about.html`, `/work` serves `work.html`, etc. No `.html` extensions needed in links or URLs.

## Making changes

- Content edits: edit the relevant `.html` file directly in GitHub web UI, commit.
- Adding a nav link: the nav is duplicated across all pages. Update each file.
- Adding a new essay: create a new `.html` file in the `writing/` folder.
- Styling updates: CSS is embedded in each page. For now, update each page individually. (A future refactor to Next.js would consolidate this.)

## Assets (to be added)

- Jake's headshot → `/images/jake.jpg` (referenced in about.html, currently placeholder)
- Acuity logo SVG → `/images/acuity-logo.svg` (optional)
- Pario screenshot → `/images/pario-screenshot.jpg` (optional, for home page Pario section)

## Domain

Primary: acuitysourcing.com → Vercel deployment
DNS managed through Squarespace (domain registration only).
