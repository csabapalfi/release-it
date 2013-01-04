---
layout: index
---

My notes for the book titled '[Release It!](http://pragprog.com/book/mnee/release-it)' by Michael T. Nygard

<ul class="posts">
  {% for post in site.posts reversed %}
    <li><a href=".{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>