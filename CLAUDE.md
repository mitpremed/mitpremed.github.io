# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static website for the MIT Pre-Medical Society (premed.mit.edu; domain set in `CNAME`), served as-is by GitHub Pages. There is no build system, package manager, linter, or test suite. Edit the files and open the `.html` pages directly in a browser (or `python3 -m http.server`) to preview. Pushing to `master` publishes the site.

## Architecture

- Plain hand-written HTML pages at the repo root (`index`, `about-us`, `guide`, `events`, `contact`, plus per-event pages `cpw`, `dph-lite`, `mixer`, `jtm-panel`). `cpw_old.html` is an archived page that is not linked from the nav.
- A single shared stylesheet, `style.css`. Fonts load from Google Fonts; icons come from the vendored `font-awesome-4.7.0/` (don't edit it). `index.html` additionally loads a Font Awesome kit script from a CDN for the newer icons (`fa-user-friends`, etc.).
- Internal links omit the `.html` extension (`href="about-us"`), which relies on GitHub Pages' clean-URL resolution. Opening pages via `file://` will break those links; use a local server that resolves extensionless paths or add `.html` temporarily.
- Static assets: `assets/` (logo, banner, PDFs), `mpsphotos/` (event/site photos), `dphslides/` (DPH Lite slide PDFs), and headshots in `headshots/` (older officers) and `YY-YY headshots/` folders (one per academic year; file names contain spaces in some folders, so quote paths).

## Things to know before editing

- **No shared templates or includes.** Every page duplicates the `<head>`, the desktop navbar (`.navBar`, including the Events dropdown), and the mobile menu (`#menuToggle`). Any nav change (adding a page, renaming an event) must be made in every HTML file. The copies have already drifted (e.g. mobile menu labels like "CPW 202w" vs "CPW 2024", and "Boston Mixer 2021" vs the dropdown's "Boston Mixer 2022"), so check each file rather than assuming they match.
- **Responsive layout is CSS-only**: the desktop navbar is hidden below 980px and the hamburger menu hidden above it (`style.css`, top of file); other breakpoints are at 800px and 1200px near the end of the file. Check both layouts when changing nav or page structure.
- **Officer roster (`about-us.html`)**: each officer is a `.people` block containing the headshot `<img>`, a hover bio in `.imgCaptionHover` (class year and course, then bio), `<h4>` name and `<h5>` title. Co-presidents are wrapped in `.people_with_padding`, followed by `<div class="break">`. Each year's new headshots go in a new `YY-YY headshots/` folder, and the markup must point at it.
- **Events (`events.html`)**: events are `.event_box` blocks (date widget in `.events_widget`, details in `.events_info`) grouped under `.event_year` headings, newest year first. The nav dropdown labels on all pages (e.g. "CPW 2024") need updating when a new event page replaces an old one.
- The `.DS_Store` files are tracked in git; don't add more to commits.
