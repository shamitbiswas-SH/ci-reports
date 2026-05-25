# Simplify Healthcare — Competitive Intelligence Reports

Auto-generated competitive intelligence reports produced by the Simplify CI Agent V6.5.

## Live site
After enabling GitHub Pages, reports are accessible at:
```
https://<your-org>.github.io/<repo-name>/
```

## Repo structure
```
/
├── index.html              ← landing page listing all reports
├── reports/
│   ├── edifecs.html        ← individual competitor reports
│   └── ...
├── .nojekyll               ← tells GitHub Pages to skip Jekyll
└── README.md
```

## How reports are added
Reports are auto-committed by the n8n CI-Report sub-workflow after each completed scan.
The workflow:
1. Reads the 10-tab Google Sheet output from the CI Agent
2. Calls Claude Opus 4.7 to write structured narrative JSON
3. Renders HTML using the Simplify Healthcare brand template
4. Commits to `reports/<competitor-slug>.html` via the GitHub API
5. Updates `index.html` to list the new report
6. Appends the new entry to the Report Registry sheet

## Caching policy
Reports expire 90 days after generation. Re-requesting an already-scanned competitor within 90 days returns the cached version — zero scan cost.

## Manual updates
To regenerate a specific report, trigger the CI Agent with `force_fresh_scan: true` on the scan form.

## Brand
Simplify Healthcare visual system. Primary blue `#105299`, gold accent `#D6B73E`. Roboto Slab for headlines, Inter for body.
