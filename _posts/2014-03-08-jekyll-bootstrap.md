---
layout: post
title: "个人建站：基于jekyll bootstrap"
description: "基于jekyll bootstrap的网站搭建"
category: "notes"
tags: [建站]
---
{% include JB/setup %}

## 0. pre
一直以来想要自己搭建一个自己的个人网站，平时可以督促自己记录一些经验以及感想，还可以重新加强自己已经退化多年的写作水平。

咱说做就做吧。

---
## 1. 域名申请
在[godaddy](http://www.godaddy.com)上申请域名，首推.com的域名。支持支付宝付款，如果在支付页面看不到支付宝支付，请看这里：[GoDaddy不支持支付宝的解决办法](http://www.dute.me/godaddy-alipay.html)，在这里推荐一个网站<http://www.dute.me/>，提供godaddy的优惠码，并且多数都支持支付宝付款。

域名解析，使用[dnspod](https://www.dnspod.cn/)提供的服务，原因是在国内godaddy的域名解析不稳定。


---
## 2. 建站方式
本文主要介绍基于[jekyll bootstrap](http://jekyllbootstrap.com/)建立一个轻量级博客的方式。至于其他框架，例如WordPress，可以参考Mac君的[趣谈个人建站](http://macshuo.com/?p=547)。提到Mac君，那是好人一个，所写的[《MacTalk人生元编程》](http://item.jd.com/11398297.html)可谓是站在技术和人文的十字路口，指导我们这些码农们努力前行啊。

[阮一峰](http://www.ruanyifeng.com)曾经在其个人博客[《搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门》](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)一文中提到了如何通过**github**的[github Pages ](http://pages.github.com)功能建立个人博客。

本博客是借助[jekyll bootstrap](http://jekyllbootstrap.com/)所建立的，如下是其官网首页的引文：

>### The Quickest Way to Blog on GitHub Pages.
>**Get a complete blog scaffold published and hosted on GitHub Pages in 3 minutes!**
>
>Jekyll-Bootstrap is a full blog scaffold for Jekyll based blogs. Don't know what [Jekyll](http://jekyllrb.com/) is? Read the [Jekyll Introduction](http://jekyllbootstrap.com/lessons/jekyll-introduction.html).
>
>Jekyll Blogs are cool because:
>
>
> * Create content in markdown or textile.
> * Manage everything with git.
> * Publish from terminal.
> * No database.
> * No hosting headaches.

于是乎，我按照着其给出的方法，去试着搭建自己的博客。

在这过程中发现了一些优秀的资源。这是一份[站点列表](https://github.com/jekyll/jekyll/wiki/Sites)，里面记录了许许多多基于jekyll方式建站的站点，以及这些站点在github上托管的**源码**。如下是一些我在这过程中发现并参考的blog。

* <http://mark.reid.name/> [(source)](https://github.com/mreid/jekyll/)
* <http://justjavac.com/> [(source)](https://github.com/justjavac/justjavac.github.com)

---
有关于github Pages的域名如何绑定到自己的独立域名，请参考这里：<https://help.github.com/articles/setting-up-a-custom-domain-with-pages>

---
## 3. 评论系统
jekyllbootstrap 中默认嵌入的社会化评论系统是[disqus](http://disqus.com)，支持facebook和twittr，在国外很流行，但在国内就不行了，原因大家都懂。

所以为了方便国内用户使用评论和分享，我们使用[多说](http://duoshuo.com)提供的评论系统。

注册用户，找到`添加新站点`-`工具`-`获取代码`，复制**通用代码**部分。

在jekyllbootstrap的工程目录的_includes/JB/comments-providers中创建一个名为`duoshuo`的文件，拷贝代码至该文件，保存。

例子如下(本例中的YOURNAME需要换成您在多说创建**多说域名**时使用的名字，网站上给出的默认代码已经帮您默认写好了)：

```
	<!-- Duoshuo Comment BEGIN -->
		<div class="ds-thread"></div>
	<script type="text/javascript">
	var duoshuoQuery = {short_name:"YOURNAME"};
		(function() {
			var ds = document.createElement('script');
			ds.type = 'text/javascript';ds.async = true;
			ds.src = 'http://static.duoshuo.com/embed.js';
			ds.charset = 'UTF-8';
			(document.getElementsByTagName('head')[0] 
			|| document.getElementsByTagName('body')[0]).appendChild(ds);
		})();
		</script>
	<!-- Duoshuo Comment END -->
```


修改_includes/JB/comments文件，复制`when`和`include`的两行，将其中的相应内容改为`duoshuo`。
	
修改_config.yaml文件，找到`comments :`，将`provider`后的值改为`duoshuo`，对应的`short_name`改为在多说创建**多说域名**时使用的名字，如下：

	provider : duoshuo
    disqus :
      short_name : ***
    duoshuo:
      short_name : YOURNAME
      
---
## 4. 

---
## 5. 结束语
   
