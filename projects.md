---
layout: page
title: Projects
subtitle: My projects..
---

<div class="posts-list">
  {% for project in site.projects %}
  <article class="post-preview">
    <a href="{{ project.url | relative_url }}">
      <h2 class="post-title">{{ project.title }}</h2>
      {% if project.subtitle %}
      <h3 class="post-subtitle">{{ project.subtitle }}</h3>
      {% endif %}
    </a>

    <div class="post-entry-container">
      <div class="post-entry">
        {{ project.content | strip_html | truncatewords: 40 }}
        <a href="{{ project.url | relative_url }}" class="post-read-more">[Projeyi İncele]</a>
      </div>
    </div>
  </article>
  {% endfor %}
</div>
