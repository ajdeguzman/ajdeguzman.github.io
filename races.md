---
layout: page
title: Races
permalink: /races/
---

{%- assign all_races = site.data.races | sort: "date" | reverse -%}
{%- assign upcoming = all_races | where: "upcoming", true -%}
{%- assign done = all_races | where_exp: "r", "r.upcoming != true" -%}
{%- assign total_km = 0 -%}
{%- for r in done -%}
  {%- assign d = r.distance | remove: "k" | plus: 0 -%}
  {%- assign total_km = total_km | plus: d -%}
{%- endfor -%}

Road, trail and ultra races — {{ done.size }} of them since
{{ done.last.date | date: "%Y" }}, about {{ total_km }}km of racing all told.
There are [photos]({{ "/races/gallery/" | relative_url }}) too.

{% if upcoming.size > 0 %}
## Upcoming

<ul class="race-list">
{%- for race in upcoming -%}
  <li>
    <span class="post-meta">{{ race.date | date: "%d %b %Y" }}</span> &raquo;
    {% if race.url %}<a href="{{ race.url }}">{{ race.name }}</a>{% else %}{{ race.name }}{% endif %}
    <span class="race-meta">{{ race.distance }}{% if race.location %} &middot; {{ race.location }}{% endif %}</span>
  </li>
{%- endfor -%}
</ul>
{% endif %}

{%- assign by_year = done | group_by_exp: "r", "r.date | date: '%Y'" -%}
{%- for year in by_year %}
<h2 class="race-year">{{ year.name }}</h2>

<ul class="race-list">
{%- for race in year.items -%}
  <li>
    <span class="post-meta">{{ race.date | date: "%d %b" }}</span> &raquo;
    {%- if race.url %}
      <a href="{{ race.url }}">{{ race.name }}</a>
    {%- else %}
      {{ race.name }}
    {%- endif %}
    <span class="race-meta">
      <span class="race-distance">{{ race.distance }}</span>
      {%- if race.location %} &middot; {{ race.location }}{% endif -%}
      {%- if race.time %} &middot; {{ race.time }}{% endif -%}
    </span>
  </li>
{%- endfor -%}
</ul>
{%- endfor -%}
