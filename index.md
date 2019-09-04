---
title: ❤
---

<style>
 .article { position: relative; padding-left: 6em; }
 .article time { position: absolute; top: 3px; left: 0; font-size: .8em; }
</style>

{% for post in site.posts %}
<p class="article">
  <a href="{{ post.url }}">{{ post.title }}</a><br>
  <small>{{ post.excerpt }}</small>
  <time>{{ post.date | date: '%Y-%m-%d' }}</time>
</p>
<hr>
{% endfor %}
