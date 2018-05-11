---
title: 首页
---

### Articles
{% for post in site.posts %}
  <time datetime="{{ post.date }}">{{ post.date | date_to_string }}</time>
  <a href="{{ post.url }}">{{ post.title }}</a>
  <br>
  <small>{{ post.excerpt }}</small>
  <hr>
{% endfor %}
