---
title: "Docker端口映射与容器互联"
date: 2018-06-18T19:16:05+08:00
draft: true
tags: ["Docker"]
---

<!--more-->

## 端口映射
### 从容器外部访问容器应用
```bash
# -P 随机映射一个49000~49900之间的端口到内部容器开发的网络端口
docker run -d -P --name web training/webapp python app.py
# 通过-p 指定端口映射
docker run -d -p 8080:5000 --name web1 training/webapp python app.py
# 查看容器日志
docker logs -f web
```


## 容器互联
> 容器的互联是一种让多个容器中应用进行快速交互的方式，它会在源和接受容器之间建立连接关系，接受容器可以通过荣启明快速访问到源容器，而不用指定具体的IP地址

### QuirckStart
```bash
# 创建数据库容器
docker run -d --name db training/postgres
# 连接到db容器
docker run -d -P --name web --link db:db training/webapp python app.py
# --link的格式为 --link name:alias 其中name是要连接的容器的名称，alias是这个连接的别名

# 查看 web的环境变量
 docker run --rm --name web2 --link db:db training/webapp env
```

