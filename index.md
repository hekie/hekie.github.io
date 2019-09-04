---
title: ❤
---

<style>
  article {
    display: inline-block;
    width: 25%;
    vertical-align: top;
  }
  article time {
    font-size: .8em;
    opacity: .8;
  }
</style>

### Articles
{% for post in site.posts %}
<article>
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <p>{{ post.excerpt }}</p>
  <p><time>{{ post.date | date: '%Y-%m-%d' }}</time></p>
</article>
{% endfor %}
