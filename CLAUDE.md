# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Class assignment (Diseño de Interfaces Web, 2º DAW): a luxury restaurant website for **Hotaru (蛍)**, a ten-seat omakase in Seki, Gifu. Deadline 2026-12-01 23:59. The brief is `docs/enunciado.pdf` (git-ignored, copyrighted).

- `web/` is the deliverable. It gets zipped and handed in, so everything the site needs must live inside it.
- Site content is **English only**. The README and commit messages are in Spanish.
- `docs/hotaru-logo.html` is the logo reference: an inline SVG on a dark background (washi text + gold 蛍), plus a light-background variant (sumi + urushi, because gold fails contrast on light backgrounds).

## Running

Plain static HTML + CSS. No build step, package manager, linter or tests. Open `web/index.html` in a browser, or serve `web/` with any static server (e.g. VS Code Live Server). Use DevTools responsive mode to check narrow widths.

## Architecture

- Four pages: `index.html` (Home), `team.html`, `menu.html` and `contact.html`. Only Home has content so far (hero + intro sections). The other three have the `<head>` and the `<header>` nav, duplicated by hand from Home, but no body content. There are no includes, so a change to the nav or the Google Fonts `<link>` must be repeated in all four files. `aria-current="page"` must sit on the current page's link.
- A single stylesheet, `web/css/style.css`, split into banner-commented sections: RESTART (reset), CUSTOM PROPERTIES, GENERAL, NAVIGATION, then one section per page (HOME SECTION → HERO, …). Keyframes go at the end.
- The CSS uses **native CSS nesting**: child selectors are written inside their parent block (`header { .nav { .pages { … } } }`). Follow that style.
- Design tokens live on `:root`. Colours: `--washi`, `--sakura`, `--sumi`, `--stone`, `--urushi`, `--gold`. There are also `--urushi-dark`, `--line` and `--ligh-text` (the misspelling is the real name). Fonts: `--font-title` (Cormorant Garamond), `--font-text` (Zen Kaku Gothic New), `--font-japanese` (Shippori Mincho). Cormorant Infant is used directly for the intro numbers. Plus `--header-height` and `--side-padding` (the shared horizontal page margin). Use these instead of raw values.
- The header is `position: sticky`, and `.hero` uses `margin-top: -80px` so it sits under the header. That value must stay in sync with `--header-height`.
- Fluid sizing uses `clamp()`. There are no `@media` queries yet. Responsive overrides are planned, including undoing the hero `h2`'s `text-wrap: nowrap`.
- Images are pre-sorted into `web/img/restaurant/`, `web/img/team/` and `web/img/dishes/`. The README also mentions `web/js/`, `docs/mockup/` and `docs/referencias/`, but those don't exist yet.
- CSS comments are written in English, often explaining the *why* (the author is learning).
