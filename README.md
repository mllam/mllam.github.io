# mllam.github.io

Source of the mllam community website, https://mllam.github.io.

## Layout

| Path | Served at | What it is |
| --- | --- | --- |
| `index.html`, `styles.css` | `/` | The community front page. Plain HTML and CSS, no build step. |
| `roadmap.toml` | `/roadmap/` | Configuration of the roadmap page, built by [github-milestone-roadmap](https://github.com/mllam/github-milestone-roadmap) during deployment. |

Other paths under mllam.github.io (e.g. `/weather-model-graphs/`) are
GitHub Pages sites of the individual package repositories and are not part of
this repository.

## Editing the front page

Edit `index.html` directly. To add a section, add a
`<section class="section">` with an `<h2>` inside `<main>` (there is a comment
marking the place). Keep the page dependency-free: no frameworks or external
scripts.

Preview locally:

```sh
python3 -m http.server 8080
```

and visit http://localhost:8080. To also preview the roadmap:

```sh
uvx github-milestone-roadmap build --config roadmap.toml --output roadmap
```

(`roadmap/` is git-ignored.)

## Deployment

The `Deploy GitHub Pages` workflow (`.github/workflows/pages.yml`) runs on every
push to `main`. It copies the front page into `_site/`, builds the roadmap into
`_site/roadmap/` with the pinned `github-milestone-roadmap` version, and
deploys `_site`.

- The roadmap's *content* (issues, PRs, milestones) is loaded live from GitHub
  in the browser, so it is always current.
- To change which repositories the roadmap shows, edit `roadmap.toml`.
- To pick up a new release of the roadmap tool, bump
  `GITHUB_MILESTONE_ROADMAP_VERSION` in the workflow.
