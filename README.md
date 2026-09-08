# NussairHroub.github.io

Source for my academic homepage: <https://nussairhroub.github.io>

It is a single-page Jekyll site built on the [Minimal Light](https://github.com/yaoyao-liu/minimal-light)
theme by Yaoyao Liu, used under the theme's CC0 1.0 Universal license (see `LICENSE`).

## Local development

Ruby comes from Homebrew and the gems are vendored under `vendor/bundle`:

```bash
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
bundle install
bundle exec jekyll serve
```

Then open <http://localhost:4000>. Jekyll rebuilds on save; the generated site goes to `_site/`,
which is not committed.

## Where to edit what

The whole page is `index.md` plus the partials it pulls in with `include_relative`.

| Section on the page | File |
| --- | --- |
| Name, position, affiliation, email, social links, avatar and favicon paths | `_config.yml` |
| About / Research Interests / News | `index.md` |
| Publications | `_data/publications.yml` |
| Experience | `_includes/experience.md` |
| Education | `_includes/education.md` |
| Projects | `_includes/projects.md` |
| Honors and Awards | `_includes/awards.md` |
| Teaching | `_includes/teaching.md` |
| Technical Skills | `_includes/skills.md` |
| Profile photo | `assets/img/avatar.jpg` |
| Browser tab icons (light / dark) | `assets/img/favicon.png`, `assets/img/favicon-dark.png` |

Publication entries live in `_data/publications.yml`; `_includes/publications.md` renders them and
does not need editing. Adding a new section means adding a file under `_includes/` and one
`include_relative` line in `index.md`.

Styles are in `_sass/minimal-light.scss` and the page shell is `_layouts/homepage.html`. The theme
supports dark mode, so avoid hardcoding text colors in the partials.

## Profile photo

`assets/img/avatar.jpg` is the headshot carried over from the previous version of this site. To change
it, drop a square image at that same path (roughly 400x400 or larger; the header crops it to a circle
and renders it at 8em).

## Publication teasers

Each entry in `_data/publications.yml` may set `image:` to a thumbnail. The theme crops it to
270x123, so a roughly 2.2:1 crop works best. The WACV paper uses `assets/img/teaser_imotion.png`.

The *Computers in Biology and Medicine* paper has no teaser: the article is closed access and no
figure is openly available to link. To add one, save a figure from the paper as
`assets/img/teaser_lung.png` and add this line to that entry:

```yaml
    image: ./assets/img/teaser_lung.png
```

Entries without an image still line up correctly — they show the venue badge alone.

## Blog (currently hidden)

The blog is built but switched off, so nothing about it is published. To turn it on, make both
changes in `_config.yml`:

1. `blog_enabled: true` — shows the pen icon in the header that links to `/blog/`.
2. Remove `- blog.md` from the `exclude:` list — otherwise the page is never generated.

`blog.md` renders the post list at `/blog/`. Posts are Markdown files in `_posts/` named
`YYYY-MM-DD-slug.md` with `layout: post`; `_drafts/example-post.md` is a template. Preview drafts
with `bundle exec jekyll serve --drafts`. With no posts the page reads "No posts yet.", so it is
worth writing one before turning the blog on.

The `_layouts/page.html` and `_layouts/post.html` layouts stay in the repo either way; they cost
nothing while the blog is off.

## Deployment

Pushing to `main` triggers `.github/workflows/pages.yml`, which builds the site with the Ruby and
Jekyll versions pinned in `Gemfile` and publishes it to GitHub Pages. Building in Actions rather than
letting GitHub run its own Jekyll means the deployed site matches what you see locally.

This requires **Settings → Pages → Build and deployment → Source: GitHub Actions** on the repository.

The workflow also fails the build if a CV PDF ever ends up in the generated site — that file is
deliberately kept off the published site and out of the repository (see `.gitignore`).
