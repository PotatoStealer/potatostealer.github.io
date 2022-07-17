---
layout: page
title: Opinions
permalink: /opinions/
---
These are posts aimed to be more serious: usually commentaries of what I notice in the news recently, or criticisms and insights about the societal problems. I try my best not to limit these topics to the Singaporean society only, but I am of course plagued by my myopic tendencies (both literally and figuratively).

It should be noted that my opinions are my own.
<hr/>    
{%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
<ul class="post-list">
  {% for post in site.categories.opinions %}
      <li>
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <a class="post-link" href="{{ post.url }}">{{ post.title | escape }}</a>
        {{ post.excerpt }}
      </li>
  {% endfor %}
</ul>