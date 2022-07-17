---
layout: page
title: Book Reviews
permalink: /books/
category: books
---
These are a series of less-serious blog entries about books that I read. Occasionally, I might decide that a book is a good enough read that spur me to write something about it, or interject with my own opinions and add on to the author's insights.

As a personal goal, I intend to read one book every month, with a 0.5 probability of this goal being successful each month.
<hr/>
{%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
<ul class="post-list">
  {% for post in site.categories.books %}
      <li>
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <a class="post-link" href="{{ post.url }}">{{ post.title | escape }}</a> 
        {{ post.excerpt }}
      </li>
  {% endfor %}
</ul>