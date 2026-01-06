---
layout: page
title: Tags
permalink: /tags/
---
{% assign tags = site.tags | sort %}

{% for tag_data in tags %}
  {% assign tag_name = tag_data | first %}
  {% assign tag_slug = tag_name | slugify %}

  <h2 id="{{ tag_slug }}">
    <a href="#{{ tag_slug }}">{{ tag_name }}</a>
  </h2>

  <ul>
    {% assign posts_by_date = tag_data[1] | sort: "date" %}
    {% for post in posts_by_date %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
{% endfor %}

