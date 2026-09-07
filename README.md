# ajdeguzman.github.io

Source for my personal site — notes, talks, projects and race logs.
Built with [Jekyll](https://jekyllrb.com/) and served by GitHub Pages.

**Live at <https://ajdeguzman.github.io>**

## Running it locally

The site is built by GitHub Pages' classic pipeline, so the `Gemfile` depends on
the `github-pages` gem rather than pinning Jekyll directly — local builds use the
exact versions GitHub deploys. Ruby is pinned in `.ruby-version`.

```sh
rbenv install 3.3.4        # once, if you don't have it
bundle install
bundle exec jekyll serve   # http://127.0.0.1:4000
```

Useful flags: `--livereload` to refresh on save, `--drafts` to include `_drafts/`,
`--future` to include posts dated ahead of now.

`_config.yml` is **not** hot-reloaded — restart the server after editing it.

Typography is Charter (body), Inter (headings and UI) and a system monospace
stack. Comments are [giscus](https://giscus.app/), backed by this repo's
GitHub Discussions. Analytics are [GoatCounter](https://www.goatcounter.com/) —
cookie-free, production only.

## Writing

Posts live in `_posts/` and need a date in the filename:

```
_posts/YYYY-MM-DD-some-title.md
```

Front matter drives where a post shows up:

```yaml
---
layout: post
title:  "A Title"
date:   2026-08-30 09:00:00 +0800
categories: life     # omit entirely to file it under Notebook
# featured: true     # marks it with a star in the list
# comments: false    # hides the comment thread on this post
---
```

`categories: life` sends a post to **Life**; anything without it lands in
**Notebook**. There's no third bucket — Talks, Projects and Races are driven by
`_data/*.yml`, not by posts.

### Drafts

Half-finished pieces go in `_drafts/` with **no date in the filename**:

```sh
$EDITOR _drafts/some-half-baked-idea.md
bundle exec jekyll serve --drafts
```

Jekyll dates a draft by its last-modified time, so there's nothing to get wrong
while you're still writing. Drafts are excluded from the build unless you pass
`--drafts`, and GitHub Pages never passes it — so a committed draft stays
unpublished. When it's ready:

```sh
git mv _drafts/some-half-baked-idea.md _posts/2026-09-01-some-half-baked-idea.md
```

Two things that fail quietly:

- **A future date is skipped without an error.** If a post doesn't appear, check
  its date against the clock (timezone included) and re-run with `--future` to
  confirm that's the cause.
- **A missing blank line before a Liquid include** lets kramdown fold the markup
  into the paragraph above and escape it. The list pages carry a note about this.

## Licence

Content and code are released under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — see [LICENSE](LICENSE).
You're welcome to reuse any of it with attribution.

The vendored theme under `_sass/minima/`, `_layouts/` and `_includes/` derives
from [minima](https://github.com/jekyll/minima) (MIT). The PDF icon in
`assets/minima-social-icons.svg` is from
[Bootstrap Icons](https://icons.getbootstrap.com/) (MIT).
