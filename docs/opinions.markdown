---
layout: page
title: Opinions
permalink: /opinions/
---
These are posts aimed to be more serious: usually commentaries of what I notice in the news recently, or criticisms and insights about the societal problems. I try my best not to limit these topics to the Singaporean society only, but I am of course plagued by my myopic tendencies (both literally and figuratively).

It should be noted that my opinions are my own.

<ul>
  {% for post in site.categories.opinions %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        {{ post.excerpt }}
      </li>
  {% endfor %}
</ul>