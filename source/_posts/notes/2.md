---
title: 笔记-Ubuntu配置
date: 2020-02-25 12:29:33
tags:
    - Ubuntu
categories:
    - 笔记
cover: https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/img-002.jpg
mp3: http://music.163.com/song/media/outer/url?id=427606780.mp3
---
**笔记小记：该篇笔记记录了个人在更换成Ubuntu18.04系统后，常用的一些配置信息**
## Python3配置
- pip换国内源  
进入到个人的家目录（`~`）下，在该目录下创建`.pip`文件夹，在`pip`文件夹下创建`pip.conf`文件，并在`pip.conf`文件下添加内容如下：
``` vim
[global]
timeout = 6000
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```
- virtualenvwrapper配置python3  
Ubuntu18.04默认只安装了python3，所以安装virtualenvwrapper后需要进行python3的配置。  
虽然python已经自带了创建虚拟环境的命令`python -m venv 虚拟环境名`，现在virtualenv和virtualenvwrapper的用处不是很大了。ㄟ( ▔, ▔ )ㄏ  
在家目录（`~`）下找到`.bashrc`文件，并添加内容如下：
``` vim
# 配置virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/workspace
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source ~/.local/bin/virtualenvwrapper.sh
# 指定virtualenv的路径
export VIRTUALENVWRAPPER_VIRTUALENV=$HOME/.local/bin/virtualenv
```
*注意：pip命令安装出来的virtualenvwrapper和virtualenv在不同的Ubuntu系统中，位置是不同的。*  
## vim配置
没啥好说的，打开`/etc/vim/vimrc`添加内容如下：
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
## JDK配置
下载Linux版的jdk  
提供一个jdk1.8的包——[jdk-8u161-linux-x64.tar.gz](https://pan.baidu.com/s/1ZCvfVAZzVPLzirRBefcn0g)  
提取码: 5rja  
解压压缩包，获的jdk的文件夹`jdk1.8.0_161`，将文件夹放到合适的位置。  
修改`/etc/profile`文件，在文件末尾添加内容如下：
``` vim
#set java env
export JAVA_HOME=/usr/lib/jdk/jdk1.8.0_161  # 记得修改成你的jdk文件夹名
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```
重新加载/etc/profile  
``` bash 
$ source /etc/profile
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
返回Java版本信息，则配置成功。
## Ubuntu换清华源
参考链接：[https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)