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
    

# 
git reset

# 仅查看提交修改的文件

    git log --stat

    # 仅查看最近一次的记录
    git log -1

    git log -1 --stat

# 参考资料
* (pro git)[https://git-scm.com/book/zh/v1]
