---
title: "Docker数据管理"
date: 2018-06-17T23:59:40+08:00
draft: true
tags: ["Docker"]
---

<!--more-->

## 数据卷(Data Volumes)
> 容器内数据直接映射到本地主机环境

- 数据卷可以在容器之间共享和重用，容器键传递数据将变得高效方便
- 对数据卷内数据修改会立马生效，无论是容器内操作还是本地操作
- 卷会一直存在，直到没有容器使用，可以安全的卸载它

### 将本地文件内容映射到nginx
```bash
# docker run -d -p 本地端口:80 --name 容器名称 -v 你需要映射的文件夹:/usr/share/nginx/html nginx
# 80是nginx默认的端口
# /usr/share/nginx/html是nginx容器默认的root目录
docker run -d -p 80:80 --name contentNginx -v $PWD/public:/usr/share/nginx/html nginx
```

- 你需要映射的文件夹:/usr/share/nginx/html后面可以加`:ro`,这样容器就不能对数据卷内容做修改了


## 数据卷容器
> 使用特定的容器维护数据卷
> 如果用户需要在多个容器之间共享一些持续更新的数据，最简单的方式是使用数据卷容器


### QuickStart
```bash
# 创建一个容器，在容器内挂载一个数据卷 `dbdata`
docker run -it  -v /dbdata --name dbdata ubuntu
# 可以在其他容器中使用--volumes-from 
docker run -it --volumes-from dbdata --name db1 ubuntu
docker run -it --volumes-from dbdata --name db2 ubuntu
# dbdata、db1、db2容器在/dbdata目录下的写入，其他容器都可以看到
```


### 使用数据卷容器备份数据
```bash
# 将数据卷容器中的数据备份到本地目录
docker run --volumes-from dbdata -v $PWD:/backup --name worker ubuntu tar cvf /backup/backup.tar /dbdata
# 这个命令有点复杂, 首先使用ubuntu创建了一个容器worker,使用--volumes-from dbdata 参数让worker容器挂载dbdata容器的数据卷，使用-v $PWD:/backup 参数来挂载本地的当前目录到worker容器的/backup目录
# worker 容器启动后，使用tar cvf /backup/backup.tar /dbdata命令来将/dbdata下的内容备份到/backup/backup.tar，也就是宿主机的当前目录下
```

### 使用数据卷容器恢复数据
```bash
# 首先创建一个带有数据卷的容器dbdata2
docker run -v /dbdata --name dbdata2 ubuntu /bin/bash
# 创建一个新的容器，挂架dbdata2的容器，并且使用ubtar 解压备份的文件到所挂载的容器卷中
docker run --volumes-from dbdata2 -v $PWD:/backup busybox tar xvf /backup/backup.tar
# 需要注意的是，这个backup.tar需要使用上面备份的backup.tar,否则不能讲backup的数据解压到/dbdata目录下
```

