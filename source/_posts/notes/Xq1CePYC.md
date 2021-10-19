---
title: 笔记-hexo博客的搭建
date: 2020-06-06 13:20:32
tags:
    - hexo
categories: 
    - 笔记
cover: https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/img-004.jpg
mp3: http://music.163.com/song/media/outer/url?id=468176711.mp3
---
### 运行docker的node容器
[笔记-Docker容器运行](../3)
### 在docker的node容器中搭建hexo博客——简单记载
1. 进入node-alpine容器，修改apk命令的数据源：  
a. 打开`/etc/apk/repositories`  
b. 将里面的`dl-cdn.alpinelinux.org`改成`mirrors.aliyun.com`，保存退出即可  
c. 执行：`apk update`  
2. 安装git、openssh-client、hexo-cli：
``` bash
$ apk add git
$ apk add openssh-client
$ npm install -g hexo-cli
```
npm淘宝源：`--registry=https://registry.npm.taobao.org`  
3. 创建博客所在的文件，进入文件中，执行初始化命令：
``` bash
$ hexo init
# 如果初始没有彻底成功，在npm下载插件的时候报错执行下面命令:
$ npm install
```
4. 去GitHub找自己喜欢的hexo主题
5. 连接到GitHub  
a. 设置git的用户和邮箱  
``` bash
$ git config --global user.name "your name"
$ git config --global user.email "your@email.com"
```
b. 生成密钥
``` bash
$ ssh-keygen -t rsa -C your@email.com
```
c. 将`~/.ssh/`目录下的`id_rsa.pub`文件内容复制到GitHub上，并测试。
``` bash
$ ssh -T git@github.com
```
当返回 "`Hi your name！you've successfully authenticated ...`"，表示你已经连接GitHub成功。
6. hexo上传到GitHub的插件——`hexo-deployer-git`  
修改博客根目录下的`_config.yml`文件  
``` yml
deploy:
  type: git
  repo: git@github.com:mrgaodi/mrgaodi.github.io.git
  branch: master
```
使用 `hexo g` && `hexo d` 进行提交  
7. 博客备份  
a. 从GitHub上把自己的仓库拉下来，进入拉取的文件夹内，将除`.git`和`.gitignore`外的文件全部清空，把本地博客文件夹下的内容copy的仓库文件夹中，编写`.gitignore`文件，选择哪些文件不上传到GitHub。  
b. git创建一个新分支
``` bash
# 新建本地分支
$ git branch hexo
# 切换到新分支
$ git checkout hexo
# 将本地分支推送到GitHub上
$ git push origin hexo
# 提交代码到GitHub上
$ git add .
$ git commit -m '提交的笔记'
$ git push origin hexo
```
附：我的`.gitinore`内容
``` vim
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
package-lock.json
yarn.lock
```