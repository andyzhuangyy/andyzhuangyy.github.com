---
layout: page
title: 记录点点滴滴
tagline: Supporting tagline
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
  <!-- date_to_string -->
    <li><span>{{ post.date | date: "%Y.%m.%d" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

---

## TODO

* 微信公众号
* gollum wiki. here
* 开始写作
* 整理简历

---
