---
title: 首页
---

<style>
  .main-content p {
    position: relative;
    padding-left: 6em;
  }
  .main-content time {
    position: absolute;
    top: 3px;
    left: 0;
    font-size: .8em;
  }
</style>

### Articles
{% for post in site.posts %}
  [{{ post.title }}]({{ post.url }})
  <br>
  <time>{{ post.date | date_to_string }}</time>
  <br>
  <small>{{ post.excerpt }}</small>
  <hr>
{% endfor %}
