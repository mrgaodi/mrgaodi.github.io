---
title: 愉快的使用ubuntu18.04——软件和环境配置篇
date: 2019-12-05 21:17:07
tags: 
    - Ubuntu18.04
    - 软件安装
top_img: 
cover: 
categories: 
    - Ubuntu18.04
    - Gnome3桌面美化
keywords: 
    - Ubuntu
    - 环境配置
    - 软件安装
description: 不美翻自己，怎么快乐的敲代码。
---

# 快速开始

## 环境

### Ubuntu配置

- 关闭Ubuntu自动更新

打开`软件和更新`，选择`更新`，将`自动检测更新`修改成`从不`，然后点击`关闭`。

![001.png]()

- 换源

``` bash
# 备份原始文件
$ sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

`/etc/apt/sources.list`修改文件内容。

{% note info %}
以下源内容是针对ubuntu18.04的，其他对应源请到清华开源软件镜像源进行查找。

ubuntu镜像源——清华源：[https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/](https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/)
{% endnote %}

``` vim
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

### JDK

下载linux系统的jdk。

提供一个jdk1.8的包——[jdk-8u161-linux-x64.tar.gz](https://pan.baidu.com/s/1ZCvfVAZzVPLzirRBefcn0g)

提取码: 5rja

到你文件的下载目录下，执行如下操作：

``` bash
# 解压文件
$ tar -xzvf jdk-8u161-linux-x64.tar.gz
# 将文件移动到/usr/lib/下
$ sudo mkdir /usr/lib/jdk
$ sudo mv jdk1.8.0_161/ /usr/lib/jdk/
```

修改`/etc/`

### Hexo博客

### Python

- pip

- virtualenvwrapper

### vim配置

## 软件

- QQ

- 网易云音乐

- VLC

- 向日葵

- 百度网盘

- WPS

- Pycharm

- Idea

- Timeshift

- Navicat Permium

- VsCode