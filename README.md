# CloudLibrary Internship Report — FCAJ Sample Style

This Hugo project reorganizes the official bilingual CloudLibrary internship report using the **Hugo Relearn** documentation theme, matching the layout pattern of the FCAJ workshop sample:

- Search box and collapsible nested sidebar
- Numbered report sections and child pages
- Breadcrumbs, table of contents, previous/next navigation
- Visited-link history and clear-history control
- English/Vietnamese language switcher
- Screenshots, architecture diagram, code snippets, and downloadable technical files

## Deploy

1. Upload all files to the root of the `Report_AWS` repository.
2. Keep `.github/workflows/hugo.yaml` in the exact hidden path.
3. In **Settings → Pages**, select **GitHub Actions**.
4. Commit to `main`; the workflow downloads the pinned Relearn theme and deploys the site.

Expected URL: `https://tjack-coder.github.io/Report_AWS/`
