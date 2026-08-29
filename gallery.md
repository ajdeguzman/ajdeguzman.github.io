---
layout: page
title: Gallery
permalink: /races/gallery/
---

{%- comment -%}
  Photos are discovered from assets/races/ at build time, so uploading a file
  is all it takes. The README lives alongside them, hence the .md exclusion.
{%- endcomment -%}
{%- comment -%} where_exp takes one condition only, so chain them. {%- endcomment -%}
{%- assign photos = site.static_files | where_exp: "f", "f.path contains '/assets/races/'" -%}
{%- assign photos = photos | where_exp: "f", "f.extname != '.md'" -%}
{%- assign photos = photos | sort: "name" | reverse -%}

Photos from the start lines, finish chutes and trails — the bits that don't fit
in the [race log]({{ "/races/" | relative_url }}).

{% if photos.size > 0 %}
<div class="gallery">
{%- for photo in photos -%}
  {%- assign base = photo.basename -%}
  {%- assign maybe_date = base | slice: 0, 10 -%}
  {%- assign parts = maybe_date | split: "-" -%}
  {%- assign has_date = false -%}
  {%- if parts.size == 3 and maybe_date.size == 10 -%}
    {%- assign yr = parts[0] | plus: 0 -%}
    {%- if yr > 1990 -%}{%- assign has_date = true -%}{%- endif -%}
  {%- endif -%}

  {%- if has_date -%}
    {%- assign slug = base | remove_first: maybe_date | remove_first: "-" -%}
  {%- else -%}
    {%- assign slug = base -%}
  {%- endif -%}

  {%- assign override = site.data.gallery[photo.name] -%}
  {%- if override -%}
    {%- comment -%} Hand-written captions are used verbatim. {%- endcomment -%}
    {%- assign caption = override -%}
  {%- else -%}
    {%- comment -%}
      Title Case the filename. Liquid has no such filter, so build it word by
      word: first and last always capitalised, minor words left lowercase.
    {%- endcomment -%}
    {%- assign words = slug | replace: "-", " " | replace: "_", " " | split: " " -%}
    {%- assign caption = "" -%}
    {%- for w in words -%}
      {%- assign lw = w | downcase -%}
      {%- if forloop.first or forloop.last -%}
        {%- assign cw = w | capitalize -%}
      {%- elsif site.title_case_minor_words contains lw -%}
        {%- assign cw = lw -%}
      {%- else -%}
        {%- assign cw = w | capitalize -%}
      {%- endif -%}
      {%- if forloop.first -%}
        {%- assign caption = cw -%}
      {%- else -%}
        {%- assign caption = caption | append: " " | append: cw -%}
      {%- endif -%}
    {%- endfor -%}
  {%- endif -%}

  {%- capture full_caption -%}
    {{ caption }}{% if has_date %} — {{ maybe_date | date: "%d %b %Y" }}{% endif %}
  {%- endcapture -%}

  <figure class="gallery-item">
    <a href="{{ photo.path | relative_url }}" title="{{ full_caption | escape }}">
      <img src="{{ photo.path | relative_url }}" alt="{{ full_caption | escape }}" loading="lazy" decoding="async">
      <figcaption>
        {{ caption }}
        {%- if has_date %}<span class="gallery-date">{{ maybe_date | date: "%d %b %Y" }}</span>{% endif -%}
      </figcaption>
    </a>
  </figure>
{%- endfor -%}
</div>
{% else %}
<p class="gallery-empty">
  No photos yet. Drop images into <code>assets/races/</code> and they'll appear
  here — see the README in that folder for the naming convention.
</p>
{% endif %}
