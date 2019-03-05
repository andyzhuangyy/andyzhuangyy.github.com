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

* gollum wiki. here
* 开始写作
* 让生活更加有节奏，坚持好习惯
* 坚持阅读
* 坚持跑步和健身
* 记录上面的过程

## 收藏

* (收藏夹)[2019/03/05/favorate]

---
