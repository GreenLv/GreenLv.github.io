# Repository Guide

## Project overview

This repository is Gerui Lv's personal academic homepage, deployed at
`https://greenlv.github.io/`. It is a Jekyll site forked from AcademicPages,
which in turn is based on Minimal Mistakes.

Keep changes incremental and low risk. Preserve the existing AcademicPages
theme, author sidebar, content, and academic presentation unless the user
explicitly requests a broader redesign.

## Sources of truth

- `_pages/about.md`: homepage content and the independently maintained six-item
  Selected Publications list.
- `_data/news.yml`: news entries. Dates use quoted `YYYY-MM` strings; the
  homepage sorts them in descending order and displays the latest six.
- `_pages/publications.md`: complete publication list. Do not replace it with a
  collection loop or force it to share a content source with the homepage.
- `_pages/cv.md`: HTML CV.
- `_data/navigation.yml`: top navigation. The site title is the Home link; the
  navigation contains only standalone pages (`Publications` and `CV`).
- `_config.yml`: canonical site metadata, author identity, URL, timezone, and
  Jekyll configuration.
- `_sass/_variables.scss`: global typography and color variables.
- `assets/css/main.scss`: site-specific visual refinements.
- `_includes/footer.html`: footer and build-date display.

Never edit `_site/`; it is generated and ignored by Git.

## Content invariants

- Canonical English identity:
  `Special Research Assistant (Postdoctoral Researcher)`.
- Canonical Chinese identity: `特别研究助理（博士后）`.
- Do not introduce `Assistant Professor` or `助理研究员`.
- Do not add recruitment or admissions language; the site owner does not have
  independent student-admission quotas.
- Keep NASG prominent on the homepage. It intentionally advertises the group
  and communicates accumulated team work.
- Keep the homepage Selected Publications list uncategorized.
- The homepage list and full Publications page are intentionally independent.
  Do not deduplicate them through includes, data files, or a shared template.
- Preserve publication wording, author order, venues, metrics, links, news,
  research content, and Technical Impacts unless a content change is explicitly
  requested.
- On the CV page, keep `Honors and Awards` before `Patents & Standards`.

## Homepage structure

Keep the homepage sections in this order:

1. About Me and Research Interest
2. Recent News
3. Research Scope of NASG
4. Open-source projects
5. Selected Publications
6. Technical Impacts

Detailed education, honors, patents, alumni, talks, internships, teaching, and
reviewing belong on the CV page rather than the homepage.

## Visual conventions

- The primary link and accent color is Royal Blue `#4169E1`; retain it unless
  the user explicitly requests a new palette.
- Link hover uses the darker blue `#274FC7`, not orange.
- Use Georgia/serif for the site title, author name, and content headings.
- Use the system sans-serif stack for body text and navigation controls.
- Base font size is 16px on small screens and 17px from the medium breakpoint.
- Keep the news panel subtle: pale blue-gray background, thin border, and a
  Royal Blue left accent.
- Publication/research tags are supporting metadata. Keep them compact and less
  visually dominant than paper titles.
- Keep the NASG table horizontally scrollable on mobile; do not allow it to
  create page-level horizontal overflow.
- Keep Selected Publications in three visual layers: title/resources/tags,
  authors, and venue. Inside its `markdown="1"` container, use explicit `<br>`
  elements for stable line breaks rather than literal backslashes.
- Favor restrained spacing, borders, and color. Avoid cards, heavy shadows,
  gradients, or decorative animations that weaken the academic style.

## Editing guidance

- Treat existing content as authoritative. Prefer moving or formatting text to
  rewriting it.
- Preserve unrelated user changes in a dirty worktree.
- Use `apply_patch` for hand edits.
- Keep navigation URLs as trailing-slash routes.
- For Markdown embedded in HTML containers, add `markdown="1"` where Kramdown
  must process Markdown syntax.
- News `content` values contain trusted repository-controlled HTML and are
  rendered as HTML on the homepage.
- Do not reintroduce AcademicPages example posts, publications, talks,
  teaching, portfolio entries, demo archive pages, or privacy boilerplate.
- Do not add a standalone Research page or Research navigation item unless the
  user reverses the current information-architecture decision.

## Build and local preview

Install dependencies when needed:

```sh
bundle install
```

Production build:

```sh
bundle exec jekyll build
```

Local preview with localhost asset URLs and expanded Sass:

```sh
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

If `_config.yml` changes while serving, restart Jekyll; configuration changes
are not reloaded automatically.

GitHub metadata warnings about a missing API token or rate limits are non-fatal
when Jekyll completes the build successfully. Do not commit dependency caches,
Bundler directories, or `_site/`.

## Required validation

For ordinary page or style changes:

1. Run `git diff --check`.
2. Run `bundle exec jekyll build`.
3. Verify `/`, `/publications/`, `/cv/`, and `/404.html`.
4. Check desktop and a roughly 390px-wide mobile viewport.
5. Confirm there is no page-level horizontal overflow.
6. Confirm the mobile navigation collapses and the NASG table scrolls within
   its own container.
7. For content moves, compare the source text and confirm nothing was silently
   omitted or rewritten.

## Footer date semantics

`{{ site.time }}` is the Jekyll build timestamp. The footer's copyright year and
`Last updated` date change only when the site is rebuilt; they do not advance
merely because a calendar day passes. This repository currently has no
scheduled GitHub Actions workflow. A push that triggers GitHub Pages, a manual
rebuild, or another Pages rebuild trigger can update the displayed date.

If the desired meaning changes from "last build" to "last substantive content
update", use an explicit maintained value in `_config.yml` instead of
`site.time`.
