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
      <a href="{{ talk.url | relative_url }}" target="_blank" rel="noopener">{{ talk.title }}</a>
    {%- else %}
      {{ talk.title }}
    {%- endif %}
    {%- if talk.pdf %}
      {%- comment -%}
        `pdf` holds either a local deck in assets/talks/ or an external slide
        URL. Only the local ones get relative_url — running it over an absolute
        URL would prepend the baseurl and break the link.
      {%- endcomment -%}
      {%- if talk.pdf contains "://" -%}
        {%- assign slides_href = talk.pdf -%}
      {%- else -%}
        {%- assign slides_href = talk.pdf | relative_url -%}
      {%- endif -%}
      <a class="talk-pdf" href="{{ slides_href }}" target="_blank" rel="noopener"
         title="Slides" aria-label="{{ talk.title | escape }} — slides"><svg class="svg-icon" aria-hidden="true" focusable="false"><use xlink:href="{{ '/assets/minima-social-icons.svg#pdf' | relative_url }}"></use></svg></a>
    {%- endif %}
    <span class="talk-venue">
      {%- if talk.event_url -%}
        <a href="{{ talk.event_url }}" target="_blank" rel="noopener">{{ talk.event }}</a>
      {%- else -%}
        {{ talk.event }}
      {%- endif -%}
      {%- if talk.location %} &middot; {{ talk.location }}{% endif -%}
    </span>
  </li>
{%- endfor -%}
</ul>
