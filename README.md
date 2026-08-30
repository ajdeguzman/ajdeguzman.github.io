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
stack. Comments are [Utterances](https://utteranc.es/), backed by this repo's
GitHub Issues. Analytics are [GoatCounter](https://www.goatcounter.com/) —
cookie-free, production only.

## Licence

Content and code are released under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — see [LICENSE](LICENSE).
You're welcome to reuse any of it with attribution.

The vendored theme under `_sass/minima/`, `_layouts/` and `_includes/` derives
from [minima](https://github.com/jekyll/minima) (MIT). The PDF icon in
`assets/minima-social-icons.svg` is from
[Bootstrap Icons](https://icons.getbootstrap.com/) (MIT).
