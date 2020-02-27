---
title: 笔记-Docker
date: 2020-02-27 13:20:32
tags:
    - docker
    - 笔记
categories: 
    - 笔记
cover: https://cdn.jsdelivr.net/gh/mrgaodi/CDN/img/img-003.jpg
mp3: http://music.163.com/song/media/outer/url?id=468176711.mp3
---
**笔记小记：该篇笔记记录了个人在简单使用docker容器时的经历**
## Docker
### 更换镜像源  
在`/etc/docker`目录下创建`daemon.json`文件，并添加如下内容：
``` vim
{
        "registry-mirrors": [
                "https://kfwkfulq.mirror.aliyuncs.com",
                "https://2lqq34jg.mirror.aliyuncs.com",
                "https://pee6w651.mirror.aliyuncs.com",
                "https://registry.docker-cn.com",
                "http://hub-mirror.c.163.com"
        ],
        "dns": ["8.8.8.8","8.8.4.4"]
}
```
### 运行MySQL数据库
``` bash
$ sudo docker run -itd --name mysql \
-v $PWD/data:/var/lib/mysql \
-p 13306:3306 --restart=always \
-e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
```
\-d：后台运行  
\-v：挂载到磁盘，数据持久化  
\-p：端口映射，docker容器的`3306`端口映射到宿主机的`13306`端口  
\-e：添加变量，使用123456作为MySQL中root用户的密码  
\--name：docker容器命名  
\--restart: 容器是否跟随docker一同启动，always同时启动。
### 运行Redis数据库  
``` bash
$ sudo docker run -itd -p 16379:6379 \
-v $PWD/data:/data --restart=always \
--name redis redis:5 redis-server \
--appendonly yes --requirepass "123456"
```
\--appendonly yes：开启Redis的AOF模式  
\--requirepass：设置Redis的密码  
进入Linux容器的命令：
``` bash
$ sudo docker exec -it redis bash
```
### 运行node容器为hexo博客
``` bash
$ sudo docker run -itd -p 14000:4000 \
-v $PWD/hexo:/root --restart=always \
--name node node:12-alpine
```
进入alpine容器的命令：
``` bash
$ sudo docker exec -it node sh
```
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
$ ssh -T git@gitnub.com
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