---
title: "使用Dockerfile创建镜像"
date: 2018-06-18T20:08:52+08:00
draft: true
tags: ["Docker"]
---

<!--more-->

## Dockerfile基本机构
### Dcokerfile 分为四部分
1. 基础镜像信息
2. 维护者信息
3. 镜像操作指令
4. 容器启动时执行指令

### 指令说明

指令 | 说明|
---|---
FROM |指定所创建镜像的基础镜像
MAINTAINER| 指定维护者信息
RUN| 运行指令
CMD | 指定启动容器时默认执行的命令
LABEL| 执行生抽镜像的元数据标签信息
EXPOSE| 声明镜像内服务所监听的端口
ENV | 指定环境变量
ADD | 复制指定的`src`路径下的的内容到容器的`dest`路径下， `src`可以为`url`; 如果为`tar`文件，会自动解压到`dest`路径下
COPY | 复制本地主机的`src`路径下的内容到镜像中的`dest`路径下;一般情况下推荐使用`COPY`而不是`ADD`
ENTRYPOINT | 指定镜像的默认入口
VALUME| 创建数据卷挂载点
USER | 指定运行容器时的用户名或UID
WORKDIR| 配置工作目录,意指执行命令的目录
ARG | 指定镜像内使用的参数
ONBUILD | 配置当所创建的镜像作为其他镜像的基础镜像时，所执行的创建操作指令
STOPSIGNAL| 容器退出的信号值
HEALTHCHECK| 如何进行健康检查
SHELL | 指定使用shell时的默认shell类型,默认值为["/bin/sh", "-c"]

## 创建镜像
```bash
docker build -t 镜像名称 Dockerfile所在路径
```

## 最佳实践
1. 多动手编写一些简单的例子实践、测试
2. 在Docker Hub上提供了大量的优秀镜像和对应的Dockerfile，阅读它们来学习
3. 选择合适的基础镜像
4. 减少镜像层数，尽量合并指令，例如多个RUN可以合成一条
5. 删除临时文件和缓存文件
5. 使用`.dockerignore`忽律不必要的文件以提高生产的速度
