---
title: "Professional Development"
layout: collection
permalink: /professional/
collection: professional
entries_layout: # list (default), grid
show_excerpts: # true (default), false
sort_by: # date (default), title or any metadata key added to the collection's documents
sort_order: # forward (default), reverse
---
Find posts related to professional development here, whether it be topic on lock picking, CTF competitions, cybersecurity, or computer science!

<html>
{% for post in site.posts %}
  {% if post.tags contains "professional" %}
    
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
