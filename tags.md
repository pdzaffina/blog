---
layout: page
title: Tags
permalink: /tags/
---

{% comment %}
    We use 'sort: "0"' to explicitly sort by the first item (index 0) 
    in each tag pair, which is the tag name.
{% endcomment %}
{% for tag in site.tags | sort: "0" %}
  {% assign tag_name = tag | first %}
  {% assign tag_slug = tag_name | slugify %}

  <h2 id="{{ tag_slug }}"><a href="#{{ tag_slug }}">{{ tag_name }}</a></h2>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}