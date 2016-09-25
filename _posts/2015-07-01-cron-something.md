---
layout: post
title: "cron"
description: ""
category: "notes"
tags: [cron]
---
{% include JB/setup %}


# 基于 crontab 实现定时任务

## 1. crontab
* 一个命令
* 依靠 cron 执行
* 通过调用一个我们设定的任务，来实现

任务如何编写，如下。

## 2. 如何写一个 crontab 任务
一个 crontab 格式一个包含6个部分，如下：

    minute hour day month day-of-week command-line-to-execute

| Field	| Range of values |
|-------|-----------------|
|minute	|0-59             |
|hour	|0-23             |
|day	|1-31             |
|month	|1-12             |
|day-of-week|	0-7 (0/7 sun. 其他)|
|command-line-to-execute|	the command |

每个域必须按照正确的顺序，不能有空格，也不能有空域，必须在同一行。

## 3. 更多例子

### 每小时

    0 * * * *

### 每2小时执行
使用 "/" 分隔

    0 */2 * * *

### 每月1日、20日早晨8点
"," 是与的意思。

    0 8 1,20 * *

### 猜猜看

    2 3 4,5 6 7

每个6月的4、5日，并且是周日的3:02分

## 4. 加上命令

例子：

    30 11 * * * /your/directory/whatever.pl

另一个例子：

    30 11 * * * /usr/bin/wget http://www.example.com/cron.php

## 5. 错误通知

不想看到任何信息

    30 11 * * * /your/directory/whatever.pl >/dev/null

添加电子邮件

    MAILTO=email@example.com
    30 11 * * * /your/directory/whatever.pl >/dev/null

电子邮件为空

    MAILTO=""

## 6. 调用cron job
* 将如上的任务配置保存到文件，例如 "crontab.conf"
* 调用

    crontab crontab.conf

调用的同时，cron命令会执行任务。

如下有关于crontab 命令。

列出所有 cron：

    crontab -l

取消任务：

    crontab -r

## 7. 参考

[1] [http://www.thesitewizard.com/general/set-cron-job.shtml](http://www.thesitewizard.com/general/set-cron-job.shtml)
