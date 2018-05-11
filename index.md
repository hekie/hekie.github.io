---
title: 首页
---

### Articles

{% for post in site.posts %}
  [{{ post.title }}]({{ post.url }})
  <br>
  <small>{{ post.date | date_to_string }}</small>
  <br>
  <small>{{ post.excerpt }}</small>
  <hr>
{% endfor %}
