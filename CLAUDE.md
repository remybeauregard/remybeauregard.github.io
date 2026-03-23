# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Personal academic website for Remy Beauregard (economics PhD candidate), deployed via GitHub Pages at `remybeauregard.com`. The site is hand-coded HTML/CSS with a Quarto-generated CV.

## Building the CV

The CV is the only file that requires a build step. It is authored in [cv.qmd](cv.qmd) and renders to both HTML and PDF:

```bash
# Render both HTML and PDF
quarto render cv.qmd

# Render only HTML
quarto render cv.qmd --to html

# Render only PDF (requires pdflatex)
quarto render cv.qmd --to pdf
```

Both `cv.html` and `cv.pdf` are committed to the repo and served directly — there is no CI/CD pipeline. Whenever `cv.qmd` is edited, both output files must be re-rendered and committed alongside the source change.

## Architecture

- **[index.html](index.html)** — Main page, fully hand-coded HTML with inline structure and `<details>`/`<summary>` elements for collapsible abstracts.
- **[styles.css](styles.css)** — Stylesheet for the main site.
- **[cv.qmd](cv.qmd)** — CV source in Quarto markdown; renders to `cv.html` and `cv.pdf`.
- **[cv-styles.css](cv-styles.css)** — CV-specific stylesheet; WCAG 2.1 Level AA compliant.
- **[Media/](Media/)** — Profile photo and research graphics.

## Key Conventions

- The CV PDF uses `pdflatex` with Mathpazo font and custom LaTeX preamble defined in `cv.qmd` frontmatter.
- `cv.html` uses `embed-resources: true`, so it is a fully self-contained file with no external dependencies.
- Accessibility: all files in the repo must comply with WCAG 2.1 Level AA. Color contrast ratios in `cv-styles.css` are documented against this standard — maintain compliance when editing any styles or HTML.
