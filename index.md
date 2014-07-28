---
layout: page
title: xephon
tagline: Documentation & Knowledge Management
---
{% include JB/setup %}

Hi, I'm Stefan, a technical writer and part-time media IT student, who is keen on information architectures and knowledge management. I write about information processing with XML- and No-XML tools and technologies.

## Recent Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
