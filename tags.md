---
layout: page
title: Tags
permalink: /tags/
---

{% for tag in site.tags | sort %}
  {% assign tag_name = tag | first %}
  {% assign tag_slug = tag_name | slugify %}

  <h2 id="{{ tag_slug }}"><a href="#{{ tag_slug }}">{{ tag_name }}</a></h2>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}