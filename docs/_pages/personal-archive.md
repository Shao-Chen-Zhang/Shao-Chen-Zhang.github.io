---
title: "Personal"
layout: collection
permalink: /personal/
collection: personal
entries_layout: # list (default), grid
show_excerpts: # true (default), false
sort_by: # date (default), title or any metadata key added to the collection's documents
sort_order: # forward (default), reverse
---

<h2>Posts</h2>
<ul>
  {% for post in site.posts %}
    {% if post.categories contains "personal" %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>
