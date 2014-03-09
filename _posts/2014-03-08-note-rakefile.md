---
layout: post
title: "Note: Rakefile"
description: "Rakefile的学习笔记"
category: "note"
tags: [ruby]
---
{% include JB/setup %}

由于需要部署基于ruby脚本的静态站点工具jekyll，所以至少需要弄懂一些基本文件的功能。

这是其一。

---

Rakefile是ruby的Makefile文件，包含可执行的ruby代码，使用ruby脚本允许的语法标准。

下面来自**rake**的manual的翻译：

>rake有如下特性：

>* Rakefile是完全标准的ruby语法定义，不需要编辑xml文件，不需要担心古怪的Makefile语法（是tab还是space？）
>* 用户可以自定义带先决条件的tasks
>* rake支持规则模式合成隐式任务  

（翻译不好请指教）

---
发现还是直接读Rakefile文件比较快。





