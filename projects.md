---
layout: page
title: Projects
permalink: /projects/
---

Things I've built:

<ul class="project-list">
{%- for project in site.data.projects -%}
  <li>
    <span class="post-meta">{{ project.year }}</span> &raquo;
    {%- if project.url %}
      <a href="{{ project.url }}" target="_blank" rel="noopener">{{ project.name }}</a>
    {%- else %}
      {{ project.name }}
    {%- endif %}
    <span class="project-meta">
      <span class="project-tech">{{ project.tech }}</span>
      {%- if project.description %} &middot; {{ project.description }}{% endif -%}
      {%- if project.collaborators %} &middot; with {{ project.collaborators }}{% endif -%}
    </span>
  </li>
{%- endfor -%}
</ul>
