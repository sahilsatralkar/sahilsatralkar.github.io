# Repository Guidelines

## Project Structure & Module Organization
This is the Jekyll site for `sahilsatralkar.com`. Content lives in `index.md`, `_pages/`, and `_posts/`; app legal/support pages live in `_pages/apps/`. Navigation is in `_data/navigation.yml`. Reuse `_layouts/*-custom.html`, `_includes/`, and the design system in `_sass/custom/`, imported by `assets/css/main.scss`. `_sass/minimal-mistakes/` contains theme styles. Publish optimized images in `assets/images/`; originals belong in `assets/images_original/`. `docs/` and `test/` are upstream theme references excluded from site builds, not application tests. Never edit generated `_site/` output.

## Build, Test, and Development Commands
- `bundle install`: install gem dependencies.
- `bundle exec jekyll serve`: preview at `http://localhost:4000`.
- `JEKYLL_ENV=production bundle exec jekyll build`: validate production output.
- `bundle exec jekyll clean`: clear generated output and caches.
- `git diff --check`: check patch whitespace.

Use a compatible Ruby explicitly when needed, e.g. `/opt/homebrew/opt/ruby/bin/bundle`; do not change the user's default Ruby. There are no npm test/lint scripts. HTMLProofer is not a declared dependency: report it unavailable rather than claiming link checks passed. Avoid bare `rake`, which runs theme-maintenance tasks and rewrites files.

## Coding Style & Naming Conventions
Follow `.editorconfig`: two spaces, UTF-8, LF, and trimmed trailing whitespace except Markdown. Use lowercase hyphenated filenames and `YYYY-MM-DD-title.md` for posts. Liquid include parameters use `name="value"`, not YAML colons. Preserve existing typography, responsive containers, and content scope.

## App Legal Pages
Preserve routes and canonical URLs. Follow sibling front matter: `page-custom`, explicit title/SEO description, locale, legal-page class, `analytics: false`, and `remove_heading_permalinks: true`. Keep native `mailto:` links with existing `email_off` guards. Verify product claims against current app code; ask about unknown operator identities or dashboard settings. Never infer them from an email address. Update effective dates on publication. Jekyll analytics flags do not control Cloudflare injection; consult `.github/CLOUDFLARE_PENDING_ACTION.md` and verify live behaviour before closing it.

## Testing Guidelines
Build, inspect changed pages on mobile/desktop, and check links, email destinations, headings, keyboard access, and relevant Light/Dark behaviour. Restart after `_config.yml` changes. Report actual checks and limitations, not historical results.

## Commit & Pull Request Guidelines
Preserve unrelated changes. Use focused imperative commit subjects. PRs should describe affected pages, verification, related issues, and visual evidence. Commit/push only when requested. Pushing `origin/master` triggers GitHub Pages publication; do not assume `main` exists. After publishing, verify the deployment and live content. Keep responses concise.
