---
layout: post
title: "git"
description: ""
category: "notes"
tags: [git]
---
{% include JB/setup %}

# tag

    git tag -l
    git checkout tags/<tag_name>


# 恢复修改
取消对文件的修改。还原到最近的版本，废弃本地做的修改。
    
    git checkout -- <file>

