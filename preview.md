---
layout: page
title: Preview
permalink: /preview/
---

{% assign now = site.time %}

{% assign preview_posts = site.posts 
  | where: "published", true 
  | where_exp: "post", "post.date > now" %}

{% if preview_posts.size > 0 %}
  {% for post in preview_posts %}
    <article class="post-preview">
      <h2>
        <a href="{{ post.url | relative_url }}">
          {{ post.title }}
        </a>
      </h2>
      <p class="post-meta">
        {{ post.date | date: "%B %-d, %Y" }}
      </p>
      <div class="post-excerpt">
        {{ post.excerpt }}
      </div>
    </article>
  {% endfor %}
{% else %}
  <p>No scheduled posts.</p>
{% endif %}
