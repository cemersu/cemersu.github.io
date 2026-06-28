---
layout: page
title: "Project Euler Solutions"
subtitle: "My algorithmic solutions and code breakdowns for Project Euler problems"
---

<div class="posts-list">
  {% for solution in site.euler_solutions %}
  <article class="post-preview">
    <a href="{{ solution.url | relative_url }}">
      <h2 class="post-title">{{ solution.title }}</h2>
      {% if solution.subtitle %}
      <h3 class="post-subtitle">{{ solution.subtitle }}</h3>
      {% endif %}
    </a>

    <div class="post-entry-container">
      <div class="post-entry">
        {{ solution.content | strip_html | truncatewords: 30 }}
        <a href="{{ solution.url | relative_url }}" class="post-read-more">[View Solution]</a>
      </div>
    </div>
  </article>
  {% endfor %}
</div>
