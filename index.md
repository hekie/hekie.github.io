---
title: 首页
---

# Articles
<ul>
{% for post in site.posts %}
<li>
  <p>
    <time datetime="{{ post.date }}">{{ post.date | date_to_string }}</time>
    <a href="{{ post.url }}">{{ post.title }}</a>
  </p>
  <p>{{ post.excerpt }}</p>
 </li>
{% endfor %}
 </ul>
