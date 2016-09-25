---
layout: post
title: "python unit test"
description: ""
category: "notes"
tags: [python]
---
{% include JB/setup %}

# cmd
    
    python -m unittest test_module.TestClass.test_method

# optionparser

# matplotlib

    import numpy as np
    import matplotlib.pyplot as plt

    x = np.arange(0, 5, 0.1);
    y = np.sin(x)
    plt.plot(x, y)


# python readline
命令行读取上下左右方向键


# virtual env
本篇快速总结几个Python的常见配置工具，包括setuptools、pip、virtualenv。

setuptools
setuptools管理Python的第三方包，将包安装到site-package下，安装的包后缀一般为.egg，实际为ZIP格式。默认从 http://pypi.python.org/pypi 下载包，能够解决Python包的依赖关系。

安装了setuptools之后即可用 easy_install 命令安装包，有多种安装方式可以选择。

    # easy_install PACKAGE          # 普通安装
    # easy_install /home/yeolar/pkg/PACKAGE.egg # 从本地或网络文件系统中安装
    # easy_install http://trac-hacks.org/svn/iniadminplugin/0.11/ # 从指定的下载路径安装
    # easy_install http://pypi.python.org/simple/PACKAGE/PACKAGE-0.1.2.4.tar.gz # 从URL源码包安装，条件是PACKAGE-0.1.2.4.tar.gz包中的根目录中必须包括setup.py文件
    # easy_install -f http://pypi.python.org/simple/ PACKAGE # 从web上面搜索包，并自动安装
    # easy_install PACKAGE==0.1.2.1 # 指定包的版本，如果指定的版本高于现已安装的版本就是升级了

    # easy_install -U PACKAGE       # 升级到最新版本，不指定版本就会升级到最新版本
    # easy_install -U PACKAGE==0.1.2.2 # 升级到指定版本

    # easy_install -m PACKAGE       # 卸载包，卸载后还要手动删除遗留文件

pip也是一个包管理工具，它和setuptools类似，如果使用virtualenv，会自动安装一个pip。

    # pip install PACKAGE           # 安装包
    # pip -f URL install PACKAGE    # 从指定URL下载安装包
    # pip -U install PACKAGE        # 升级包

virtualenv是一个Python环境配置和切换的工具，可以用它配置多个Python运行环境，和系统中的Python环境隔离，即所谓的沙盒。沙盒的好处包括：

解决库之间的版本依赖，比如同一系统上不同应用依赖同一个库的不同版本。
解决权限限制，比如你没有 root 权限。
尝试新的工具，而不用担心污染系统环境。

    $ virtualenv py-for-web

这样就创建了一个名为py-for-web的Python虚拟环境，实际上就是将Python环境克隆了一份。然后可以用 source py-for-web/bin/activate 命令来更新终端配置，修改环境变量。接下来的操作就只对py-for-web环境产生影响了，可以使用 pip 命令在这里安装包，当然也可以直接安装。

    $ source py-for-web/bin/activate    # 启用虚拟环境
    $ deactivate                        # 退出虚拟环境

