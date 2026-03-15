---
layout: page
title: AI
permalink: /ai/
---
Corralling my thoughts on AI as I work through it in the real world.

{% assign ai_posts = site.posts | where: "ai", true | sort: "date" | reverse %}

{% if ai_posts.size > 0 %}
  <ul>
    {% for post in ai_posts %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
        <span class="post-date"> | {{ post.date | date: "%-m/%-d/%y" }}</span>
      </li>
    {% endfor %}
  </ul>
{% else %}
  <p>No AI posts yet.</p>
{% endif %}