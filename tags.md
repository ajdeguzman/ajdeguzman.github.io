---
layout: page
title: Topics
description: Browse Aj De Guzman's writing by topic.
permalink: /tags/
---

{% assign sorted_tags = site.tags | sort %}

{% if sorted_tags.size > 0 %}
<nav class="tag-index" aria-label="All topics">
  {% for tag in sorted_tags %}
    {% assign tag_name = tag[0] %}
    {% assign tag_posts = tag[1] %}
    <a class="tag-link" href="#{{ tag_name | slugify }}">
      {{ tag_name | replace: "-", " " }}
      <span class="tag-count">{{ tag_posts.size }}</span>
    </a>
  {% endfor %}
</nav>

<div class="tag-sections">
  {% for tag in sorted_tags %}
    {% assign tag_name = tag[0] %}
    {% assign tag_posts = tag[1] | sort: "date" | reverse %}
    <section class="tag-section" id="{{ tag_name | slugify }}">
      <h2>{{ tag_name | replace: "-", " " }}</h2>
      <ul class="notebook-list">
        {% for post in tag_posts %}
          <li>
            <span class="post-meta">{{ post.date | date: "%d %b %Y" }}</span> &raquo;
            <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
          </li>
        {% endfor %}
      </ul>
    </section>
  {% endfor %}
</div>
{% else %}
<p>No topics yet.</p>
{% endif %}
