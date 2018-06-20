---
title: "Docker搭建MySQL服务"
date: 2018-06-20T19:27:36+08:00
draft: true
---

<!--more-->

``` bash
# 版本可以自己定义
docker pull mysql:5.7
# 运行一个实例
docker run -d --name some-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=你的密码 mysql:5.7
```
