---
layout: page
title: Tags
permalink: /tags/
---

### Tags

{% for tag in site.tags %}
  <h2><a href="#{{ tag | first | slugify }}">{{ tag | first }}</a></h2>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}