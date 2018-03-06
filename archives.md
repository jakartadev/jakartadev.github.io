---
layout: archive
title: Archives
permalink: /archives/
---

{% for post in site.posts %}
  {% if post.type == "digest" or post.type == "blog" %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
    <p>{{post.description}}</p>
  {% endif %}
{% endfor %}


