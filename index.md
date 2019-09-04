---
title: ❤
---

<style>
  .page-header {
    display: none;
  }
  
  ul { font-size: 0; }
  
  li {
    display: inline-block;
    width: 25%;
    font-size: 1.25rem;
    vertical-align: top;
  }
  
  @media screen and (max-width: 960px) { li { width: 33.33334% } }
  @media screen and (max-width: 640px) { li { width: 50% } }
  @media screen and (max-width: 320px) { li { width: 100% } }
  
  small {
    display: block;
    font-size: .8em;
  }
  
  time {
    font-size: .6em;
    opacity: .8;
  }
</style>

# Hekie
<ul>
{% for post in site.posts %}
<li>
  <a href="{{ post.url }}">{{ post.title }}</a>
  <small>{{ post.excerpt }}</small>
  <time>{{ post.date | date: '%Y-%m-%d' }}</time>
</li>
{% endfor %}
</ul>
