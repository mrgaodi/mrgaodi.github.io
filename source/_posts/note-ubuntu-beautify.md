---
title: 笔记-Ubuntu美化
date: 2020-02-25 15:11:47
tags:
    - Ubuntu
    - 笔记
categories: 
    - 笔记
cover: https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/img-001.jpg
mp3: http://music.163.com/song/media/outer/url?id=430685732.mp3
---
**笔记小记：该篇笔记记录了个人在换成Ubuntu18.04系统后，对系统的美化过程**
- 安装gnome-tweak-tool  
``` bash 
$ sudo apt install gnome-tweak-tool
```
- 安装gnome-shell-extensions  
``` bash 
$ sudo apt install gnome-shell-extensions
```
- 安装gnome-shell-extension-dashtodock  
``` bash
$ sudo apt install gnome-shell-extension-dashtodock
```
安装完以上3个软件后，重启下电脑 
1. 找到安装好的“`优化`”软件，点“`扩展`”，打开“`User themes`”插件，在“`优化`”首页，选择主题、图标和shell的样式。  
|![](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/ubuntu-beautify-001.png)|![](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/ubuntu-beautify-002.png)|  
|:---:|:---:|  
2. 在“`扩展`”中找到“`Dash to dock`”，点“`⚙`”，取消“`面板模式：延伸到屏幕边缘`”的勾选。———*注意：不要打开该扩展，不然会出现两个dock。*
|![](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/ubuntu-beautify-003.png)|![](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/ubuntu-beautify-004.png)|  
|:---:|:---:|  
3. 下载桌面主题和图标  
gnome主题下载网址：[https://www.gnome-look.org/](https://www.gnome-look.org/)  
我使用的主题和图标：  
桌面主题是：[McMojave](https://www.pling.com/s/Gnome/p/1275087/)  
图标主题：[Papirus](https://www.pling.com/s/Gnome/p/1166289/)  
shell主题：McMojave 自带的shell主题  
4. 美化结果：
|![](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/ubuntu-beautify-005.png)|![](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/ubuntu-beautify-006.png)|  
|:---:|:---:|  
- 终端  
打开本地的终端配置文件`~/.bashrc`，按以下内容修改
``` vim
if [ "$color_prompt" = yes ]; then
    # PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ ' 原本的配置
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;36m\]>\[\033[00m\] \[\033[01;34m\]\W\[\033[00m\] \[\033[01;32m\]\$\[\033[00m\] ' 修改之后的配置
else
    # PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ ' 原来的配置
    PS1='${debian_chroot:+($debian_chroot)}> \W \$ ' 修改之后的配置
fi
```
\[\033[01;34m\]：字符颜色  
\W：终端上只显示当前文件夹的名字  
\w：显示全部文件路径  
\h：机器名  
\u：用户名  
- 修改登陆界面的背景  
选择一张喜欢的图片放到`/usr/share/backgrounds/`目录下。  
打开`/etc/alternatives/gdm3.css`，找到`lockDialogGroup`对其进行修改。
``` vim
#lockDialogGroup {
    /* background: #2c001e url(resource:///org/gnome/shell/theme/noise-texture.png); */
    background: #2c001e url(file:///usr/share/backgrounds/xxx.jpg);  /*你选择的图片的路径*/
    background-repeat: no-repeat; /* repeat */
    background-size: cover; /*新增*/
    background-position: center; /*新增*/
    }
```  
重启电脑，再次打开时你就会发现登陆界面的背景已经变成了你选择的图片了。
