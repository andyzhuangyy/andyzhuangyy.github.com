---
layout: post
title: "shell"
description: ""
category: "notes"
tags: [shell]
---
{% include JB/setup %}

# 重定向
./siege_test_by_concurrent.sh add.url > ../logs/result/siege_add_8http_1redis.log 2>&1
cmd > file 2 >&1
