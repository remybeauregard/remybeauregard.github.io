# remybeauregard.github.io

Personal academic website for Remy Beauregard, PhD candidate in Economics at UC Davis, deployed via GitHub Pages at [remybeauregard.com](http://www.remybeauregard.com). Hand-coded HTML/CSS with a Quarto-generated CV.

## Site Structure

| File / Folder | Purpose |
|---|---|
| `index.html` | Main page (About, Research, Teaching sections) |
| `styles.css` | Stylesheet for the main site |
| `cv.qmd` | CV source — renders to `cv.html` and `cv.pdf` |
| `cv.html` | Self-contained CV (committed, served directly) |
| `cv.pdf` | PDF CV (committed, served directly) |
| `cv-styles.css` | CV-specific stylesheet |
| `Media/` | Profile photo and research graphics |
| `CNAME` | Custom domain configuration for GitHub Pages |

There is no CI/CD pipeline. All build outputs are committed directly to the repository.

### Main Page (`index.html`)

Three sections:
- **About** — bio, profile photo, contact links
- **Research** — publications, working papers, and ongoing projects, each with a collapsible abstract toggle (JavaScript, `aria-expanded`)
- **Teaching** — instructor-of-record courses, TA history, and student reviews

Navigation includes links to Research, Teaching, the HTML CV, and social icons (LinkedIn, Bluesky, AllTrails, GitHub).

## Building the CV

The CV is authored in `cv.qmd` and must be rendered with [Quarto](https://quarto.org/) whenever it changes. Both output files must be committed alongside any source change.

```bash
# Render both HTML and PDF
quarto render cv.qmd

# Render only HTML
quarto render cv.qmd --to html

# Render only PDF (requires pdflatex)
quarto render cv.qmd --to pdf
```

The HTML output uses `embed-resources: true` — it is fully self-contained with no external dependencies. The PDF uses `pdflatex` with Mathpazo font and a custom LaTeX preamble defined in the `cv.qmd` frontmatter.

## Accessibility (WCAG 2.1 Level AA)

All materials in this repository must comply with [WCAG 2.1 Level AA](https://www.w3.org/TR/WCAG21/). This is a firm requirement, not a suggestion.

**What this means in practice:**

- **Color contrast** — All text/background combinations must meet the minimum contrast ratios (4.5:1 for normal text, 3:1 for large text). Documented ratios in `cv-styles.css` must be maintained when editing any styles.
- **Images** — All `<img>` elements require descriptive `alt` text. Research graphics embedded in abstracts must have alt text that conveys the finding, not just the chart type.
- **Interactive elements** — Abstract toggle buttons use `aria-expanded` and `aria-controls` attributes; these must be preserved when modifying the toggle behavior.
- **Semantic HTML** — Use appropriate heading hierarchy, landmark elements (`<header>`, `<main>`, `<footer>`, `<section>`), and `<nav>` for navigation.
- **Language** — The `lang="en"` attribute must be present on all HTML documents.
- **Links** — All links must have discernible text. Icon-only links (social icons in the nav) use `aria-label` and `title` attributes; SVG icons use `aria-hidden="true"`.
- **Footer** — The site footer includes an accessibility contact (`rebeauregard@ucdavis.edu`) for users who cannot access content due to a disability. This must remain on all pages.

### PDF Accessibility

PDFs present additional accessibility challenges compared to HTML. The existing PDF in `Media/` (`research fellows write-up.pdf`) has been processed through an external PDF tagging accessibility program. **For any new documents, HTML format is strongly preferred** — it is significantly easier to maintain WCAG compliance in HTML than in PDF, and HTML documents can be authored and validated directly in this workflow.

If a PDF must be used, it should be run through a PDF accessibility checker and tagging tool before being committed.

## Adding or Updating Content

**New research paper** — Add a `<li class="paper">` block inside the appropriate `<ul class="paper-list">` in `index.html`. Include a unique `id` on the abstract element and wire it to the toggle button via `aria-controls`. Use descriptive `alt` text on any embedded figures.

**New media file** — Place images in `Media/`. PNGs are used for research graphics. Prefer HTML over PDF for any linked documents. Favicon files were generated with [favicon.io](https://favicon.io/favicon-generator/) and are also stored in `Media/`.

**CV changes** — Edit `cv.qmd`, then run `quarto render cv.qmd` and commit all three files (`cv.qmd`, `cv.html`, `cv.pdf`) together.

**Style changes** — Verify color contrast ratios after any color edits. The CSS custom properties in `styles.css` and `cv-styles.css` define the full color palette — changes there affect the entire site or CV respectively.
