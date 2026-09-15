---
layout: page
title: Life
description: Personal notes from Aj De Guzman about travel, running, food, books, outdoor adventures, and life away from the keyboard.
permalink: /life/
---

{% comment %}
  Anything with `categories: life` in its front matter lands here instead of
  the Notebook.

  NB: keep a blank line before the include. Without one, kramdown folds the
  list into the paragraph above and escapes the markup.
{% endcomment %}

The non-technical half — travel, food, things I've been reading, and whatever
else is going on away from a keyboard.

{% include post-list.html posts=site.categories.life empty="Nothing here yet — first entry coming soon." %}
