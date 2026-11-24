# hjalves.dev

Source for [hjalves.dev](https://hjalves.dev), Humberto Alves' personal blog and project site. The site contains articles about software development, open-source projects, and related experiments.

The site is built with [Hugo](https://gohugo.io/) and uses a customised copy of the [Tania](https://github.com/WingLim/hugo-tania) theme in `themes/tania/`. The theme is part of this repository; edit it directly.

## Requirements

- [Hugo Extended](https://gohugo.io/installation/) `0.165.0` or later
- [Dart Sass](https://sass-lang.com/install/) (the theme's stylesheets need it; on Arch: `pacman -S dart-sass`)
- Git

The deployed site uses Hugo `0.165.0` and Dart Sass `1.108.2`, as configured in [`.github/workflows/pages.yml`](.github/workflows/pages.yml).

## Getting started

Clone the repository:

```bash
git clone https://github.com/hjalves/hjalves-dev.git
cd hjalves-dev
```

Start the local development server:

```bash
hugo server -D
```

Open the local URL printed by Hugo, usually `http://localhost:1313/`. The `-D` flag includes draft content.

## Writing content

Create a new post with Hugo's default archetype:

```bash
hugo new posts/2026/09/my-post.md
```

Edit the generated front matter and content, then set `draft: false` when the post is ready to publish. Existing posts live under `content/posts/`, organized by year and month. Project entries live under `content/projects/`.

## Building

Generate the production site with:

```bash
hugo
```

The generated files are written to `public/`. The deploy workflow builds the same directory, with `--gc --minify` added. Generated files in `public/` and `resources/_gen/` are ignored by Git.

## Repository layout

```text
content/       Pages, posts, and project entries
themes/tania/  Tania theme (customised)
static/        Files copied directly to the generated site
config.toml    Hugo site configuration
archetypes/    Templates for new content
.github/       GitHub Actions deploy workflow
```

## Deployment

The site is deployed to GitHub Pages by the [`pages.yml`](.github/workflows/pages.yml) GitHub Actions workflow. Every push to `main` (or a manual run) builds the site with Hugo Extended `0.165.0` and Dart Sass `1.108.2`, and publishes `public/`.
