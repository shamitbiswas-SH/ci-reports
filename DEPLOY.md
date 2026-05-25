# Deploy to GitHub Pages — 5 minute setup

## Step 1: Create a GitHub repo
1. Go to github.com → New repository
2. Name it something like `ci-reports` or `competitive-intel-reports`
3. **Public or private?** GitHub Pages on a private repo requires GitHub Enterprise / GitHub Pro. For most teams, the practical options are:
   - **Public repo** (free Pages, but reports visible to anyone with the URL) — fine if reports are not confidential
   - **Private repo** with GitHub Pro/Enterprise — recommended for competitive intel
   - **Private repo** with no Pages — store files for archival, view via raw GitHub URLs (less polished but works)
4. Don't initialize with README (we have one already)

## Step 2: Push the files
From the unzipped folder containing these files:
```bash
cd ci-reports
git init
git add .
git commit -m "Initial CI reports — Edifecs"
git branch -M main
git remote add origin git@github.com:<your-org>/<repo-name>.git
git push -u origin main
```

## Step 3: Enable GitHub Pages
1. Repo → Settings → Pages
2. Source: "Deploy from a branch"
3. Branch: `main` / `/ (root)`
4. Save
5. Wait ~30 seconds for first deploy

## Step 4: Visit the live site
`https://<your-username>.github.io/<repo-name>/`

You should see the landing page with the Edifecs report card. Click into the Edifecs report to see the full 10-tab competitive intel deliverable.

## What's next — auto-publishing from n8n

Once you've validated the HTML quality, the next build is the **CI-Report n8n sub-workflow** that:
1. Fires after CI-Synthesis completes
2. Calls Opus 4.7 to write structured narrative JSON
3. Renders the HTML using this template
4. Commits the new report to `reports/<competitor>.html` via GitHub API
5. Updates `index.html` to add the new report card
6. Appends a row to the Report Registry sheet

You'll need:
- A GitHub Personal Access Token (PAT) with `repo` scope
- Add the PAT to n8n credentials
- The CI-Report.json sub-workflow (I'll build it once this static version is approved)
