Here’s exactly what you do (step-by-step)
1. Open your generate_cases.py on GitHub
Go to your repository, open generate_cases.py, and click the pencil icon.

2. Scroll all the way down to the end of the case_data list
You’ll see the last entry is res-gestae. It looks like this:

python
    {
        "id": "res-gestae",
        "title": "Res Gestae (Doctrine)",
        "citation": "Hearsay Exception",
        "summary": 'Res Gestae is an exception to the hearsay rule...',
        "impact": 'Officers may document spontaneous statements...',
        "source": "Common Law Doctrine — Hearsay Exception"
    }
]
3. Add a comma after the } of the last entry, then paste your new case
Important: add a comma , after the closing } of res-gestae, then paste your new dictionary.

Example – let’s say you received a suggestion for a new case: Smith v. State. You would change the end of the list from this:

python
    {
        "id": "res-gestae",
        "title": "Res Gestae (Doctrine)",
        "citation": "Hearsay Exception",
        "summary": '...',
        "impact": '...',
        "source": "Common Law Doctrine — Hearsay Exception"
    }
]
to this (added comma and new block):

python
    {
        "id": "res-gestae",
        "title": "Res Gestae (Doctrine)",
        "citation": "Hearsay Exception",
        "summary": '...',
        "impact": '...',
        "source": "Common Law Doctrine — Hearsay Exception"
    },
    {
        "id": "smith-v-state",
        "title": "Smith v. State",
        "citation": "123 U.S. 456 (2026)",
        "summary": "Officers may not search a vehicle based solely on the odor of burnt popcorn.",
        "impact": "Requires additional articulable facts beyond a lawful traffic stop to justify a vehicle search.",
        "source": "SCOTUS, 123 U.S. 456 (2026)"
    }
]
4. (Optional but recommended) Also update the categories list
If you’re using the updated generate_cases.py I gave earlier (which auto-updates index.html), you also need to add your new case ID to the categories_config list at the top of the file.

Find the category you want (e.g., 'Traffic Stops & Vehicle Searches') and add your new ID:

python
categories_config = [
    {
        "name": "Traffic Stops & Vehicle Searches",
        "icon": "🚗",
        "cases": ["whren-v-us", "carroll-v-us", "arizona-v-gant", "pennsylvania-v-mimms", "maryland-v-wilson", "smith-v-state"]
    },
    # ... rest of categories
]
5. Commit the changes
Scroll down, write a commit message like “Add new case: Smith v. State”.

Click Commit changes.

What happens next?
GitHub Actions (if you set it up) will run automatically.

It will:

Generate cases/smith-v-state.html (using the data you added).
(If using the new script) Update the category list in index.html so the new case appears on your homepage.
GitHub Pages redeploys – your new case is live at https://your-site/cases/smith-v-state.html.

to get website to update, go to dev tools - application - storage - clear website data.  return to the webpage and click ctrl+shift+r and the page should reload showing the update.
