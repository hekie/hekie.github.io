---
title: 首页
---

<style>
  .article {
    position: relative;
    padding-left: 6em;
  }
  .article time {
    position: absolute;
    top: 3px;
    left: 0;
    font-size: .8em;
  }
</style>

### Articles
{% for post in site.posts %}
<p class="article">
  <time>{{ post.date | date_to_string }}</time>
  <a href="{{ post.url }}">{{ post.title }}</a>
  <br>
  <small>{{ post.excerpt }}</small>
 </p>
 <hr>
 {% endfor %}
