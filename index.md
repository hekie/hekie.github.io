---
title: ❤
---

<style>
  .page-header {
    display: none;
  }
  
  article {
    display: inline-block;
    width: 25%;
    vertical-align: top;
  }
  
  article time {
    font-size: .8em;
    opacity: .8;
  }
  
  @media screen and (max-width: 320px) {
    article { width: 100% }
  }
  
  @media screen and (max-width: 640px) {
    article { width: 50% }
  }
</style>

<header>
  <h1>Hekie</h1>
</header>
{% for post in site.posts %}
<article>
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p>{{ post.excerpt }}</p>
  <p><time>{{ post.date | date: '%Y-%m-%d' }}</time></p>
</article>
{% endfor %}
