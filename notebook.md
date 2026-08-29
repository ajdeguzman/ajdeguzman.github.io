---
layout: page
title: Notebook
permalink: /notebook/
---

{% comment %}
  Notebook is the default bucket: every post except those filed under `life`.
  An article needs no category to land here, and gets `categories: life` to
  move across.

  NB: keep a blank line before the include. Without one, kramdown folds the
  list into the paragraph above and escapes the markup.
{% endcomment %}

Here I write up what I'm working on, what I'm learning, and the odd thing worth
remembering — notes from talks, things I've broken and fixed, and whatever else
seems useful later.

{% include post-list.html posts=site.posts exclude="life" empty="Nothing here yet — first entry coming soon." %}
