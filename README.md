# CaseLaw-LE — Police Case Law Reference

A static reference guide of case law for law enforcement, hosted on GitHub Pages. Case files are generated from `generate_cases.py` by a GitHub Actions workflow.

## How to add a case (admin workflow)

The site no longer relies on Formspree. Submissions now flow through **GitHub Issues** into an **admin page** that lets you review, edit, and approve cases — approved cases auto-publish.

### The flow
1. A user submits the form on the homepage (`index.html`) or reference page (`caselaw.html`). It saves to `localStorage` and, when an admin token is active in the browser, creates a GitHub Issue labeled `case-submission` / `status: pending`.
2. The admin opens **`admin.html`** (e.g. `https://<your-username>.github.io/CaseLaw-LE/admin.html`), signs in with a token, and sees the pending queue.
3. On each submission the admin can **Edit**, **Approve**, **Reject**, or **Delete**.
4. **Approve** appends the case to `submissions.json`, which triggers the GitHub Actions workflow to regenerate all case pages and the homepage. The case goes live automatically — no manual HTML editing.

## Flagging a case as inaccurate (public → admin)

Every case page has a **🚩 Flag this case as inaccurate** button and a short legal disclaimer noting that user-submitted content may not be independently verified.

1. A visitor clicks the flag button, types a reason, and submits.
2. If an admin token is active in that browser session, the flag becomes a GitHub Issue labeled `case-flag` / `status: pending`.
3. Otherwise it is saved to the browser's `localStorage` (`caseFlags`) and shows up in the admin page's **Local flags** section.
4. On `admin.html`, the **🚩 Case flags** section lists pending flags. The admin can **✅ Resolve** (marks `status: resolved` and posts a comment) or **🗑 Dismiss** it. Local flags can be **⬆ Send to GitHub** or dismissed.

## Editing or deleting existing cases (admin workflow)

The admin page also has an **✏️ Existing cases** section listing every published case.

1. Open `admin.html` and sign in.
2. Scroll to **Existing cases** and click a case to expand it.
3. Edit the **Title, Citation, Source, Category, Summary**, or **Impact on Law Enforcement**, then click **💾 Save edits** — or click **🗑 Delete case** to remove it entirely.
4. Each case also has a **Submitted by** field showing who submitted it, so you know who to check with if a correction is needed.
5. Changes are written to `edits.json`, which triggers the GitHub Actions workflow to regenerate the site (updating the homepage, reference page, and the individual case page). Edits to existing cases are stored as overrides in `edits.json` and applied on top of the base data in `generate_cases.py`.

> **Credit on case pages:** user-submitted cases show a small "Submitted by" credit with the submitter's initials on the case file page. Internally-authored cases show no credit line.

### Creating a GitHub token for the admin page
1. GitHub → Settings → Developer settings → **Personal access tokens → Fine-grained tokens** → *Generate new token*.
2. Repository access: **Only select repositories** → `Port-Arthur-Police-Department/CaseLaw-LE`.
3. Permissions:
   - **Issues: Read and write** (to read/manage pending submissions)
   - **Contents: Read and write** (to commit approved cases to `submissions.json`)
4. Generate and copy the `github_pat_…` token.
5. Open `admin.html`, paste the token, and sign in. The token lives **only in that browser session** (`sessionStorage`) and is never saved to the repo.

> **Security note:** Because no token is embedded in the public site, a submission made on a browser with no active admin token is saved locally and appears in the admin page's "Local submissions" section. From there you can send it to GitHub or approve it directly. (For truly public cross-browser submission without a token, a small backend such as a Cloudflare Worker would be required — a possible future improvement.)

## Manual edits (still supported)

To add or edit a case directly, edit `generate_cases.py` — the `categories_config` and `case_data` lists. After this, the "Generate Case Files" action should run and rebuild the site. New case files are added to the `/cases` folder and `index.html` / `caselaw.html` are updated to reflect the changes.

## Seeing updates

To get the website to update, go to DevTools → Application → Storage → clear site data. Return to the webpage and click **Ctrl+Shift+R** — the page should reload showing the update. (This is because of the service worker's cache-first behavior.)

## Notes / known issues

- The old online form submission (Formspree) has been replaced by the admin workflow above.
- Badges and all icon/favicon assets live in `/assets` (including the PWA manifest `assets/site.webmanifest`). If you add a new case file or asset, remember to add it to the `urlsToCache` list in `sw.js` and bump `CACHE_NAME`.
