Adding a new case – your new workflow
Edit generate_cases.py directly on GitHub:

Open the file, click the pencil icon.

Scroll down to the case_data list.

Add a new dictionary entry (copy an existing one and change the values).

Important: the "id" must be unique and match the filename you want (e.g., "new-case" → cases/new-case.html). Use only lowercase letters, numbers, and hyphens.

Commit the change (with a message like “Add new case: …”).

The GitHub Action will automatically start and:

Run generate_cases.py

Create/update all HTML files in the cases/ folder (including your new one).

Commit and push the updated cases/ folder back to your repo.

Wait 1‑2 minutes for GitHub Pages to redeploy – your new case is live at https://your-username.github.io/repo/cases/new-case.html.

4. (Optional) Update the category list in index.html
Your index.html has hard‑coded categories (categories array in JavaScript). If you want the new case to appear in a specific category, you must also edit index.html and add the new id to that category’s cases array.

How to do that on GitHub:

Open index.html, click the pencil icon.

Find the categories array (near the bottom of the file).

Locate the category you want, and add your new id to its cases list (e.g., 'new-case').

Commit the change. This will not trigger the Action (because you didn’t change generate_cases.py), but it updates the directory page immediately.
