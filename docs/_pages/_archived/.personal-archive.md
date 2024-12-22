---
title: "Personal Interests"
layout: collection
permalink: /personal/
collection: personal
entries_layout: # list (default), grid
show_excerpts: # true (default), false
sort_by: # date (default), title or any metadata key added to the collection's documents
sort_order: # forward (default), reverse
---
Find posts on topics of personal interest here, discussing topics from comics, music, literature, philosophy and art!


<html>
{% for post in site.posts %}
  {% if post.tags contains "personal" %}
    
    <h2> 
      <a href="{{ post.url }}"> 
        {{ post.title }} 
      </a>
    </h2>

    <small> 
      {{ post.excerpt }} 
    </small>
    
  {% endif %}
{% endfor %}
</html>
