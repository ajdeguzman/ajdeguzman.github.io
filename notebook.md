---
layout: page
title: Notebook
description: Technical notes from Aj De Guzman about software development, integration, machine learning, and computer science.
permalink: /notebook/
---

{% comment %}
  Notebook is the default bucket: every post except those filed under `life`.
  An article needs no category to land here, and gets `categories: life` to
  move across.

  NB: keep a blank line before the include. Without one, kramdown folds the
  list into the paragraph above and escapes the markup.
{% endcomment %}

Notes from work and school, things I'm learning, and problems I've worked through.

{% include post-list.html posts=site.posts exclude="life" empty="No posts yet." %}
