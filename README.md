# ENV3210 — Aquatic Sciences Course Website

Course website for ENV3210 Aquatic Sciences at the University of Guyana. Built with [Quarto](https://quarto.org) and deployed to GitHub Pages.

## Adding / Updating Lecture Slides

1. Name your file `Week_XX_Lecture.pptx` (e.g., `Week_03_Lecture.pptx`)
2. Drop it into `materials/lectures/`
3. Commit and push — the site rebuilds automatically

## Data Science Module Materials

The data science slides and handouts are synced automatically from the private [Data-Science-Module](https://github.com/arjoon0202/Data-Science-Module) repository via GitHub Actions. When new rendered HTML files are pushed to that repo, trigger a rebuild of this site (or wait for the daily scheduled build).

The sync uses the `DS_MODULE_PAT` secret (a GitHub Personal Access Token with access to the private repo).

## Triggering a Manual Rebuild

Go to **Actions** > **Build and Deploy Website** > **Run workflow** on the `main` branch.

## Local Preview

```bash
quarto preview
```

This renders the site locally and opens it in your browser with live reload.

## Project Structure

```
_quarto.yml              # Quarto website configuration
custom.scss              # Design system theme (fonts, colors, layout)
index.qmd                # Landing page
schedule.qmd             # 13-week schedule with material links
resources.qmd            # Curated learning resources
ENV3210_Syllabus.html    # Standalone syllabus (kept as a static asset)
materials/
  lectures/              # Manually uploaded PPTX files
  slides/                # DS module Revealjs HTML (auto-populated by CI)
  handouts/              # DS module handout HTML (auto-populated by CI)
.github/workflows/
  publish.yml            # CI/CD: clone DS repo, build site, deploy to Pages
```

## Technical Notes

- **DS module HTML files are never processed by Quarto.** They contain embedded OJS/webR JavaScript that breaks if re-rendered. The GitHub Action copies them into `_site/` after `quarto render` completes.
- **The syllabus HTML is kept as a static asset.** It can be shared as a standalone document if needed.
- **Material links degrade gracefully.** The schedule page uses JavaScript to check link availability and shows "Coming soon" for materials not yet uploaded.
