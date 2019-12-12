---
title: 我的ubuntu18.04——软件和环境配置篇
date: 2019-12-05 21:17:07
tags: 
    - Ubuntu
    - 环境配置
top_img: 
cover: 
categories: 
    - Ubuntu
    - 环境配置
keywords: 
    - Ubuntu
    - 环境配置
    - 软件推荐
description: 环境配置是开发的基础
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

修改`/etc/apt/sources.list`文件内容。

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

更新源：

``` bash
$ sudo apt update
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

修改`/etc/profile`文件，在文件末尾添加如下内容：

``` vim
#set java env
export JAVA_HOME=/usr/lib/jdk/jdk1.8.0_161  # 记得修改成你的jdk文件夹名
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

重新加载`/etc/profile`

``` bash
source /etc/profile
```

注册服务并建立软链接

``` bash
$ update-alternatives --install /usr/bin/java java /usr/lib/jdk/jdk1.8.0_161/bin/java 300
$ update-alternatives --install /usr/bin/javac javac /usr/lib/jdk/jdk1.8.0_161/bin/javac 300
```

查看安装是否成功：

``` bash
$ java -version
java version "1.8.0_161"
Java(TM) SE Runtime Environment (build 1.8.0_161-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.161-b12, mixed mode)
```

### Hexo

``` bash
# 安装git
$ sudo apt install git
# 安装nodejs
$ sudo apt install nodejs
# 安装npm
$ sudo apt install npm
# 使用npm安装hexo-cli
$ npm install -g hexo-cli
```

### Python

- pip换源

创建pip配置文件

``` bash
$ mkdir ~/.pip
$ touch ~/.pip/pip.conf
```

添加配置信息

``` vim
[global]
timeout = 6000
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```

- virtualenvwrapper

安装virtualenv/virtualenvwrapper

``` bash
$ pip install virtualenv
$ pip install virtualenvwrapper
```

在`~/.bashrc`文件中配置virtualenvwrapper

``` vim
# 配置virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/workspace
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source ~/.local/bin/virtualenvwrapper.sh
# 指定virtualenv的路径
export VIRTUALENVWRAPPER_VIRTUALENV=$HOME/.local/bin/virtualenv
```

重新使用`.bashrc`配置文件

``` bash
source ~/.bashrc
```

### vim配置

在`/etc/vim/vimrc`文件的末尾添加下文内容

``` vim
" 配置
" 开启文件检测
filetype indent on
" 缩进
set autoindent
set tabstop=4
set shiftwidth=4
set expandtab
set softtabstop=4
" 外观
set nu
set textwidth=80
set ruler
" 搜索
set showmatch
set hlsearch
set incsearch
set ignorecase
```

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