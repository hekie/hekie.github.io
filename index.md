---
title: 首页
---

### Articles
<ul>
{% for post in site.posts %}
<li>
  <time datetime="{{ post.date }}">{{ post.date | date_to_string }}</time>
  <a href="{{ post.url }}">{{ post.title }}</a>
  <br>
  <small>{{ post.excerpt }}</small>
 </li>
{% endfor %}
 </ul>
