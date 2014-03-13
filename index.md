---
layout: page
title: 庄永耀的网志
tagline: Supporting tagline
---
{% include JB/setup %}

记录生活中的点点滴滴...
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

---


[**点击这里订阅**](http://zhuangyongyao.com/atom.xml)
---


---
## To-Do
a lot of things to do.
change theme...
