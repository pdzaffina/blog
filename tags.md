---
layout: page
title: Tags
permalink: /tags/
---

{% comment %}
    The 'sort' filter applied to a hash sorts by the key (tag name).
    This is the most stable and compatible way to alphabetically sort tags 
    in older Jekyll versions like those used by GitHub Pages.
{% endcomment %}

{% assign tags = site.tags | sort %}

{% for tag_data in tags %}
  {% assign tag_name = tag_data | first %}
  {% assign tag_slug = tag_name | slugify %}

  <h2 id="{{ tag_slug }}"><a href="#{{ tag_slug }}">{{ tag_name }}</a></h2>
  <ul>
    {% comment %}
        We keep the inner loop as is, using tag_data[1] for the posts array.
    {% endcomment %}
    {% for post in tag_data[1] %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
