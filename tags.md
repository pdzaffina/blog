---
layout: page
title: Tags
permalink: /tags/
---

{% comment %}
    1. 'to_a' converts the site.tags hash into an array.
    2. 'sort: "0"' sorts the array alphabetically by the tag name (index 0).
{% endcomment %}
{% assign sorted_tags = site.tags | sort: "0" | to_a %}

{% for tag in sorted_tags %}
  {% assign tag_name = tag | first %}
  {% assign tag_slug = tag_name | slugify %}

  <h2 id="{{ tag_slug }}"><a href="#{{ tag_slug }}">{{ tag_name }}</a></h2>
  <ul>
    {% comment %}
        1. 'tag[1]' is the array of posts for the current tag.
        2. 'sort: "date"' sorts the posts by date.
        3. '| reverse' flips the order to show the newest post first (descending chronological order).
    {% endcomment %}
    {% for post in tag[1] | sort: "date" | reverse %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%Y-%m-%d" }}</li>
    {% endfor %}
  </ul>
{% endfor %}