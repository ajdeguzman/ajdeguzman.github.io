---
layout: page
title: Notebook
permalink: /notebook/
---

Here I write up what I'm working on, what I'm learning, and the odd thing worth
remembering — notes from talks, things I've broken and fixed, and whatever else
seems useful later. Newest first.

<ul class="notebook-list">
{%- for post in site.posts -%}
  <li>
    <span class="post-meta">{{ post.date | date: "%d %b %Y" }}</span> &raquo;
    <a href="{{ post.url | relative_url }}" title="{{ post.title | escape }}">{{ post.title | escape }}</a>
    {%- if post.featured %} <span class="featured" title="Featured">&#9733;</span>{%- endif -%}
  </li>
{%- else -%}
  <li>Nothing here yet — first entry coming soon.</li>
{%- endfor -%}
</ul>
