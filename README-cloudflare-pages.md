# Deploying cheatki/cadsim-mkii to Cloudflare Pages

This repository appears to be a plain static site (index.html, styles.css). Below are two ways to deploy to Cloudflare Pages, and the GitHub Action included in this PR supports Option B.

Option A — Cloudflare Pages (recommended via UI integration)

1. In the Cloudflare Dashboard go to "Pages" → "Create a project".
2. Authorize and connect your GitHub account and select the `cheatki/cadsim-mkii` repository.
3. Set build settings:
   - Framework preset: None (Static)
   - Build command: (leave blank)
   - Build output directory: `./` or `.` (if UI requires a value, use `.`)
   - Branch: `main`
4. Save & deploy. Cloudflare Pages will run builds and deploy on every push to the configured branch.

Option B — Cloudflare Pages via GitHub Actions (this PR)

1. Create an API Token in Cloudflare:
   - Cloudflare Dashboard → My Profile → API Tokens → Create Token
   - Choose "Create custom token".
   - Permissions: at minimum
     - Account: Read
     - Pages: Edit
   - Restrict the token to the specific Account (recommended).
   - Copy the token.

2. Add the following repository Secrets in your GitHub repo:
   - `CF_PAGES_API_TOKEN` — token you created.
   - `CF_ACCOUNT_ID` — your Cloudflare account ID (Dashboard → Overview).
   - `CF_PAGES_PROJECT_NAME` — the Pages project name as configured in Cloudflare (e.g., `cadsim-mkii`).

3. This workflow publishes the repository root (`./`) to the Pages project on every push to `main`.
   - If your site needs a build step (npm, hugo, etc.), add a build step in the workflow and set `directory:` to the build output folder.

Notes and tips
- If you prefer the simplest flow, use the Cloudflare UI integration (Option A). It will create the necessary deploy pipeline and manage the token for you.
- For custom domains and environment variables, configure those in the Pages dashboard after the first deployment succeeds.
