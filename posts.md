---
layout: page
title: Posts
permalink: /posts/
---

{% for post in site.posts %}
<a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%B %e, %Y" }})
{% endfor %}
