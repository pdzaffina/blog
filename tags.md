---
layout: page
title: Tags
permalink: /tags/
---

{% comment %}
    1. 'to_a' converts the site.tags hash into an array of arrays (e.g., [["tag-name", [posts...]], ...]).
    2. 'sort: "0"' then sorts that array alphabetically by the string at index 0 (the tag name).
{% endcomment %}
{% assign sorted_tags = site.tags | sort: "0" | to_a %}

{% for tag in sorted_tags %}
  {% assign tag_name = tag | first %}
  {% assign tag_slug = tag_name | slugify %}

  <h2 id="{{ tag_slug }}"><a href="#{{ tag_slug }}">{{ tag_name }}</a></h2>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}