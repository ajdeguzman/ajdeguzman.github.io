---
layout: page
title: Tags
description: Browse Aj De Guzman's writing by tag.
permalink: /tags/
---

{% assign sorted_tags = site.tags | sort %}

{% if sorted_tags.size > 0 %}
<ul class="tag-index" aria-label="All tags">
  {% for tag in sorted_tags %}
    {% assign tag_name = tag[0] %}
    {% assign tag_posts = tag[1] %}
    <li>
      <a class="tag-link" href="#tag-{{ tag_name | slugify }}">
        {{ tag_name }}
        <span class="tag-count" aria-label="{{ tag_posts.size }} {% if tag_posts.size == 1 %}post{% else %}posts{% endif %}">{{ tag_posts.size }}</span>
      </a>
    </li>
  {% endfor %}
</ul>

<div class="tag-sections">
  {% for tag in sorted_tags %}
    {% assign tag_name = tag[0] %}
    {% assign tag_posts = tag[1] | sort: "date" | reverse %}
    <section class="tag-section" id="tag-{{ tag_name | slugify }}">
      <h2>{{ tag_name }}</h2>
      <ul class="notebook-list">
        {% for post in tag_posts %}
          <li>
            <span class="post-meta">{{ post.date | date: "%d %b %Y" }}</span> &raquo;
            <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
          </li>
        {% endfor %}
      </ul>
      <a class="tag-section-close" href="{{ '/tags/' | relative_url }}">&larr; All tags</a>
    </section>
  {% endfor %}
</div>
{% else %}
<p>No tags yet.</p>
{% endif %}
