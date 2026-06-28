---
layout: page
title: Project Euler Solutions
subtitle: My solutions for some PE problems
---

<div class="posts-list">
  {% for item in site.[koleksiyon_adi] %}
  <article class="post-preview">
    <a href="{{ item.url | relative_url }}">
      <h2 class="post-title">{{ item.title }}</h2>
      {% if item.subtitle %}
      <h3 class="post-subtitle">{{ item.subtitle }}</h3>
      {% endif %}
    </a>

    <div class="post-entry-container">
      <div class="post-entry">
        {{ item.content | strip_html | truncatewords: 30 }}
        <a href="{{ item.url | relative_url }}" class="post-read-more">[Devamını Oku]</a>
      </div>
    </div>
  </article>
  {% endfor %}
</div>
