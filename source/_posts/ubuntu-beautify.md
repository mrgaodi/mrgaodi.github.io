---
title: 我的ubuntu18.04——美化篇
date: 2019-11-27 17:02:32
tags: 
    - Ubuntu
    - 系统美化
top_img: https://s2.ax1x.com/2019/12/03/QQuKXQ.png
cover: https://s2.ax1x.com/2019/12/03/QQul0s.md.png
categories: 
    - Ubuntu
    - 系统美化
keywords: 
    - Ubuntu
    - Gnome桌面
    - 系统美化
description: 不美翻自己，怎么快乐的敲代码。
---

{% note warning %}
本篇所写的桌面美化过程是基于Gnome3桌面环境，至于Gnome2桌面是否适用还需要大家自己动手试验了。
{% endnote %}

- - - 

**先来上两张最终结果**

{% gallery %}
![](https://s2.ax1x.com/2019/12/03/QQuQmj.png)
![](https://s2.ax1x.com/2019/12/03/QQul0s.png)
{% endgallery %}

- - -

# 快速开始

## 美化主题

### 安装&quot;**优化**&quot;工具

首先安装&quot;**gnome-tweak-tool**&quot;，使你可以更换桌面主题、图标、鼠标样式等等。通过以下代码进行下载：

``` bash
$ sudo apt install gnome-tweak-tool
```

安装完成之后你会看到一个名字是&quot;**优化**&quot;的软件。如下图，图标和我的应该不一样，我已经修改了图标的主题。

<img src="https://s2.ax1x.com/2019/12/03/QQnvY6.png" width="100"/>

之后点击打开，出现下图界面，可以在里面选择需要使用的主题了。

<div id="gnome-tool">
<img src="https://s2.ax1x.com/2019/12/03/QQnxfK.png" width="400"/>
</div>

{% note info %}
不过，此时你的shell主题应该是不能修改的，他会展示一个&quot;**⚠**&quot;，这时你就需要安装下面的gnome插件了。
{% endnote %}

### 安装&quot;**gnome-shell-extensions**&quot;插件

``` bash
$ sudo apt install gnome-shell-extensions
```

安装完成之后，打开&quot;**优化**&quot;软件，点击&quot;*扩展* &quot;，会出现很多插件（没有安装之前，应该是只有3个插件，缺少我们需要的），找到&quot;*User themes* &quot;这个插件，打开它。

<img src="https://s2.ax1x.com/2019/12/03/QQukTI.png" width="400"/>

{% note info %}
如果在你的&quot;*扩展* &quot;中没有出现很多插件，重启下电脑看看吧。
{% endnote %}

这时，你就会发现之前的shell主题选择框的&quot;**⚠**&quot;已经消失了，可以选择shell主题了，就像上面的[<i class="fa fa-link" aria-hidden="true">图片</i>](#gnome-tool)一样。

## 美化dock

- 安装&quot;**dashtodock**&quot;插件

``` bash
$ sudo apt install gnome-shell-extension-dashtodock
```

该插件的作用是将&quot;**dock**&quot;改称类似Mac的，不让收藏夹延伸到屏幕的。

{% gallery %}
![](https://s2.ax1x.com/2019/12/03/QQuEkt.png)
![](https://s2.ax1x.com/2019/12/03/QQump8.png)
{% endgallery %}

- 打开&quot;**优化**&quot;软件，点击&quot;*扩展* &quot;，找到&quot;*dashtodock* &quot;这个插件，点击他的设置按钮&quot;**⚙**&quot;。

<img src="https://s2.ax1x.com/2019/12/03/QQuVtP.png" width="400"/>

{% note info %}
如果在你的&quot;*扩展* &quot;中没有找到&quot;*dashtodock* &quot;这个插件，重启下电脑就好了。
{% endnote %}

- 将&quot;*面板模式：延伸到屏幕边缘* &quot;的这个复选框勾掉，此时就会只包住你的收藏夹了。

<img src="https://s2.ax1x.com/2019/12/03/QQuZff.png" width="400"/>

{% note info %}
如果你的**dock**出现了两个——一个dock下又覆盖了一个dock，可能是你打开了&quot;*dashtodock* &quot;这个插件造成的，把他关掉就好了。
{% endnote %}

{% gallery %}
![](https://s2.ax1x.com/2019/12/03/QQuimd.png)
![](https://s2.ax1x.com/2019/12/03/QQuu6g.png)
{% endgallery %}

## 选择主题

到这里，所需要的插件已经安装好了，现在需要创建存储主题的文件夹了。

``` bash
$ mkdir ~/.local/share/themes/
$ mkdir ~/.local/share/icons/
```

`themes`：保存桌面主题、shell主题。

`icons`：保存图标主题。

到[gnome主题 <i class="fa fa-external-link" aria-hidden="true"></i>][gnome-themes]的下载网站进行各种主题的下载。之后，将下载的主题解压后，放到对应的文件夹目录下，你就可以到&quot;**优化**&quot;中选择你下载的主题了。

<img src="https://s2.ax1x.com/2019/12/03/QQuCOH.png" width="400"/>

[gnome-themes]: https://www.gnome-look.org/

可能会下载很慢，可以去github上找，几乎有所有的gnome主题。

我所使用的主题：

桌面主题是：[McMojave <i class="fa fa-external-link" aria-hidden="true"></i>](https://www.pling.com/s/Gnome/p/1275087/)

图标主题：[Papirus <i class="fa fa-external-link" aria-hidden="true"></i>](https://www.pling.com/s/Gnome/p/1166289/)

shell主题：[McMojave <i class="fa fa-external-link" aria-hidden="true"></i>](https://www.pling.com/s/Gnome/p/1275087/) 自带的shell主题

## 美化终端

个人是很讨厌终端中“用户名@机器名 全路径”，所以对其进行了修改，让终端的展示类似于zsh。效果图：

{% gallery %}
![修改前](https://s2.ax1x.com/2019/12/03/QQu17n.png)
![修改后](https://s2.ax1x.com/2019/12/03/QQu8kq.png)
{% endgallery %}

打开本地的终端配置文件`~/.bashrc`，找到这几行，在vim（命令行模式下）中输入`/ if [ "$color_prompt" = yes ];`可以快速定位到此处。

<img src="https://s2.ax1x.com/2019/12/03/QQuplD.png" width="500"/>

对其进行修改

``` vim
if [ "$color_prompt" = yes ]; then
    # PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ ' 原本的配置
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;36m\]>\[\033[00m\] \[\033[01;34m\]\W\[\033[00m\] \[\033[01;32m\]\$\[\033[00m\] ' 修改之后的配置
else
    # PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ ' 原来的配置
    PS1='${debian_chroot:+($debian_chroot)}> \W \$ ' 修改之后的配置
fi
```

 `\[\033[01;34m\]`：字符颜色

 `\W`：终端上只显示当前文件夹的名字

{% note info %}
终端上所展示的一共是6个字符，&quot;>空格\W空格\$空格&quot;，每一个都要进行颜色设置，不然下一个字符会继承上一个字符的颜色。最后一个空格的颜色会影响你输入的命令的颜色，最好设置成不显示颜色。
{% endnote %}

修改完成后回到终端，输入`source ~/.bashrc`，就可以看到改变了。

## 修改登陆界面的背景

- 选择一张喜欢的图片放到`/usr/share/backgrounds/`目录下。

``` bash
$ sudo cp ~/图片/xxx.jpg /usr/share/backgrounds/
```

- 打开`/etc/alternatives/gdm3.css`，找到`lockDialogGroup`对其进行修改。

``` css
#lockDialogGroup {
    /* background: #2c001e url(resource:///org/gnome/shell/theme/noise-texture.png); */
    background: #2c001e url(file:///usr/share/backgrounds/xxx.jpg);  /*你选择的图片的路径*/
    background-repeat: no-repeat; /* repeat */
    background-size: cover; /*新增*/
    background-position: center; /*新增*/
    }
```

- 重启电脑，再次打开时你就会发现登陆界面的背景已经变成了你选择的图片了，截图不太好截取，就不再放了。
