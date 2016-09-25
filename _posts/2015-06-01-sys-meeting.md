---
layout: post
title: "error code"
description: ""
category: "notes"
tags: [error code]
---
{% include JB/setup %}

# error code
open api

## douban
两种返回码， http status code + 通用error code
http 级的code 和业务级code 会不会有冲突？


## weibo 
分错误等级，分模块，错误码

## baidu

## taobao
按区间划分


## baige say
1. 利于开发debug
2. 辅助解决问题
3. 方便于处理情况

## 协议
oAuth, 和业务级接口协议分开

## 业界其他开放平台

## 我们目前的情况
目前应用和协议隔离的状况, 都是返回200
随后定....


# unit test
之后是一个重点
上线依赖这个ut，保证安全
自动化
mock
代码覆盖

* 使用依赖注入的方式而不是全局变量的方式

内部的接口用ut的方式，不要用integrate的方式
* 数据库测试 
* web service 
比较难，不容易用unit test来写.


## <phpunit-book>



