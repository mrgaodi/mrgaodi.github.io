---
title: 笔记-Docker容器运行
date: 2020-02-27 13:20:32
tags:
    - docker
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
- 拉取mysql5.7的镜像
``` bash
$ sudo docker pull mysql:5.7
```
mysql5.7的配置文件：[my.cnf](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/file/my.cnf)  
- 运行一个mysql5.7镜像的容器
``` bash
$ sudo docker run -itd \
--name=mysql \
-v $PWD/MySQL/data:/var/lib/mysql \
-v $PWD/MySQL/config/my.cnf:/etc/mysql/my.cnf \
-p 13306:3306 \
--restart=always \
--privileged=true \
-e MYSQL_ROOT_PASSWORD=123456 \
mysql:5.7
```
\-d：后台运行  
\-v：挂载到磁盘，数据持久化  
\-p：端口映射，docker容器的`3306`端口映射到宿主机的`13306`端口  
\-e：添加变量，使用123456作为MySQL中root用户的密码  
\-\-name：docker容器命名  
\-\-restart: 容器是否跟随docker一同启动，always同时启动。  
\-\-privileged：赋予容器root用户真正的root权限  
- 进入mysql容器的命令：
``` bash
$ sudo docker exec -it mysql bash
```
### 运行Redis数据库  
- 拉取redis5的镜像
``` bash
$ sudo docker pull redis:5-alpine
```
- 从GitHub上获取对应版本的redis配置文件   
reids的GitHub地址：<https://github.com/antirez/redis>
将文件放到指定位置。($PWD/Redis/conf/redis.conf)，修改配置文件的配置。
- 运行一个redis5镜像的容器
``` bash
$ sudo docker run -itd \
-p 16379:6379 \
-v $PWD/Redis/data:/data \
-v $PWD/Redis/conf/redis.conf:/etc/redis/redis.conf \
--restart=always \
--privileged=true \
--name=redis \
redis:5-alpine \
redis-server /etc/redis/redis.conf
```
- 进入redis容器的命令：
``` bash
$ sudo docker exec -it redis sh
```
### 运行node容器
- 拉取node12的镜像
``` bash
$ sudo docker pull node:12-alpine
```
- 运行一个node12镜像的容器
``` bash
$ sudo docker run -itd -p 14000:4000 \
-v $PWD/hexo:/root --restart=always \
--name node node:12-alpine
```
- 进入alpine容器的命令：
``` bash
$ sudo docker exec -it node sh
```
### 运行flink容器
- 拉取flink的镜像
``` bash
$ sudo docker pull flink:1.9.3-scala_2.11
```
- flink的配置文件  
[flink-conf.yaml](https://cdn.jsdelivr.net/gh/mrgaodi/CDN/file/flink-conf.yaml)
- 创建docker的桥接网络
``` bash
$ sudo docker network create flink-net -d bridge
```
- 运行flink容器（jobmanager）
``` bash
$ sudo docker run -itd --name=flink-jmr \
-p 18081:8081 \
-e JOB_MANAGER_RPC_ADDRESS=flink-jmr \
--network=flink-net \
-v $PWD/jmr/flink-conf.yaml:/opt/flink/conf/flink-conf.yaml \
flink:1.9.3-scala_2.11 jobmanager
```
- 运行flink容器（taskmanager）
``` bash
$ sudo docker run -itd --name=flink-tmr01 \
-e JOB_MANAGER_RPC_ADDRESS=flink-jmr \
--network=flink-net \
-v $PWD/tmr01/flink-conf.yaml:/opt/flink/conf/flink-conf.yaml \
flink:1.9.3-scala_2.11 taskmanager
```
\-\-network：容器所在网络，互相间可以通过名称进行访问。  
\-\-JOB_MANAGER_RPC_ADDRESS：jobmanager服务的地址
- 进入flink容器的命令：
``` bash
$ sudo docker exec -it flink-jmr bash
```