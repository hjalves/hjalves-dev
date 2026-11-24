# hjalves.dev

Source for [hjalves.dev](https://hjalves.dev), Humberto Alves' personal blog and project site. The site contains articles about software development, open-source projects, and related experiments.

The site is built with [Hugo](https://gohugo.io/) and uses the [Tania](https://github.com/hjalves/hugo-tania) theme as a Git submodule.

## Requirements

- [Hugo Extended](https://gohugo.io/installation/) `0.165.0` or later
- Git, including submodule support

The deployed site uses Hugo `0.165.0`, as configured in [`netlify.toml`](netlify.toml).

## Getting started

Clone the repository and initialize the theme submodule:

```bash
git clone --recurse-submodules https://github.com/hjalves/hjalves-dev.git
cd hjalves-dev
```

If the repository was cloned without submodules, initialize it with:

```bash
git submodule update --init --recursive
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

The generated files are written to `public/`. Netlify runs the same `hugo` command and publishes that directory. Generated files in `public/` and `resources/_gen/` are ignored by Git.

## Repository layout

```text
content/       Pages, posts, and project entries
layouts/       Site-specific Hugo templates
themes/tania/  Tania theme submodule
static/        Files copied directly to the generated site
config.toml    Hugo site configuration
netlify.toml   Netlify build and deployment settings
archetypes/   Templates for new content
```

## Deployment

The site is deployed through Netlify. The configured build settings are:

- Build command: `hugo`
- Publish directory: `public`
- Hugo version: `0.165.0`

Pushes to the configured Netlify repository trigger a new deployment.