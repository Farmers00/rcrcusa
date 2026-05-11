# AGENTS.md

This is a compact guide for autonomous agents working on the RC RC USA website.

## Environment & Build
- **Hugo Version:** `0.123.7` Extended edition is required to match GitHub Actions.
- **Node.js:** `v22` (to match CI).
- **Execution:** Always use the global `hugo` command (`hugo server` for dev, `hugo` to build). Do **NOT** install or use `hugo-bin` or `npx hugo`.
- **Dependencies:** Run `npm install` to ensure PostCSS and Tailwind CSS are available.
- **Testing:** No automated tests. Verify changes by running `hugo` to ensure the build succeeds without template or PostCSS errors.

## Directories & Asset Processing
- **`content/`**: Markdown files (`_index.md` is the homepage). Edit content here rather than hardcoding in HTML layouts.
- **`layouts/`**: Go templates. `_default/baseof.html` contains the master shell (including SEO and JSON-LD).
- **`assets/images/`**: Put all images here so Hugo can process them. Use `resources.Get` and `.Resize "WIDTHx webp q80"` to generate optimized WebP responsive images.
- **`static/`**: Only for assets that completely bypass Hugo processing (e.g., vanilla JS in `static/js/main.js` and favicons).

## Quirks & Constraints
- **Hugo Deprecation:** Keep using `languageCode` in `hugo.toml` and `.Site.LanguageCode` in templates. Do **not** update it to `locale`, because the pinned `v0.123.7` version requires `languageCode` and will fail if changed.
- **Styling:** The site uses Tailwind CSS. Apply utility classes directly in templates. Avoid adding custom CSS unless using `@apply` in `assets/css/main.css`.
- **Data Files:** Leaderboards and slideshow images are driven by JSON files in `data/`. Slideshow images referenced in JSON should be processed via `resources.Get` in the layouts.
