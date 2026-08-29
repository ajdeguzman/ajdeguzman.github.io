---
layout: page
title: Talks
permalink: /talks/
---

Talks I've given at meetups, conferences and universities — mostly on
Integration, MuleSoft, AI, and building a career in tech.

<ul class="talk-list">
{%- for talk in site.data.talks -%}
  <li>
    <span class="post-meta">{{ talk.date }}</span> &raquo;
    {%- if talk.url %}
      <a href="{{ talk.url | relative_url }}">{{ talk.title }}</a>
    {%- else %}
      {{ talk.title }}
    {%- endif %}
    <span class="talk-venue">
      {%- if talk.event_url -%}
        <a href="{{ talk.event_url }}">{{ talk.event }}</a>
      {%- else -%}
        {{ talk.event }}
      {%- endif -%}
      {%- if talk.location %} &middot; {{ talk.location }}{% endif -%}
    </span>
  </li>
{%- endfor -%}
</ul>
