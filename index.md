---
layout: default
title: Dean.Q的菜园子
tagline: 积淀
---
{% for post in site.posts %}
- ### [{{ post.title }}]({{ post.url }}) <time>{{ post.date | date: '%Y-%m-%d'}}</time>

  {{post.summary}}

  [全文阅读 &raquo;]({{ post.url }})
{% endfor %}
