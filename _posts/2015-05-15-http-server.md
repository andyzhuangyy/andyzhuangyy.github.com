---
layout: post
title: "http server"
description: ""
category: "notes"
tags: [tcp, http]
---
{% include JB/setup %}


# timeout
在tcp协议上层封装应用层协议的时候，往往会遇到对端不响应，导致「假死」的情况，此时应该在封装的协议层，设定超时机制，超时后抛出异常，由调用者去决定如何处理。一般此种情况下会将当前连接关闭。
