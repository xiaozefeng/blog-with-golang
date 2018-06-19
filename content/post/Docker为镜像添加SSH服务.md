---
title: "Docker为镜像添加SSH服务"
date: 2018-06-18T22:20:17+08:00
draft: true
---

<!--more-->

## 基于commit命令
1. 准备工作

```bash
docker run -it ubuntu:14.04 /bin/bash
```

2. 安装和配置SSH服务

```bash
# 安装SSH
apt-get update
apt-get install openssh-server -y
# 如果要正常使用SSH服务，必须存在/var/run/sshd,手动创建它 mkdir -p /var/run/sshd
# 启动SSH服务
/usr/sbin/sshd -D &
# 查看22端口
netstat -tunlp
# 修改SSH安装配置，取消pam登录限制
sed -ri 's/session   required    pam_loginuid.so/#session required     pam_loginuid.so/g' /etc/pam.d/sshd
# 将本地的公钥添加到~/.ssh/authorized_keys文件中
mkdir root/.ssh
vi root/.ssh/authorized_keys
# 创建自动启动SSH的脚本
vi /run.sh
chmod +x /run.sh
# 启动run.sh的内容是
#!/bin/bash
/usr/sbin/sshd -D
# 最后退出容器
exit
```

3. 保存镜像

```bash
# 使用commit命令提交镜像 
docker commit 容器id ssh:ubuntu
# 使用镜像
docker run -p 10022:22 -d sshd:ubuntu /run.sh
# 查看运行后的容器
docker ps
# 通过ssh访问10022端口来登录容器
ssh 本地ip -p 10022
```

## 使用Dockerfile创建
1. 在本地创建一个目录

```bash
mkdir sshd_ubuntu
cd sshd_ubuntu
touch Dockerfile run.sh
```

2. 编写run.sh脚本和authorized_keys

```bash
# 在run.sh中输入
#!/bin/bash
/usr/sbin/sshd -D
```

3. 编写Dockerfile(推荐)

```Dockerfile
# 设置基础镜像
FROM ubuntu:14:04


# 执行更新命令
RUN apt-get update

# 安装ssh服务
RUN apt-get install -y openssh-server
RUN mkdir -p /var/run/sshd
RUN mkdir -p /root/.ssh

# 取消pam限制
sed -ri 's/session   required    pam_loginuid.so/#session required     pam_loginuid.so/g' /etc/pam.d/sshd

# 复制配置文件到响应的位置，并且赋予脚本可执行权限
COPY authorized_keys /root/.ssh/authorized_keys
COPY run.sh /run.sh
RUN chmod 755 /run.sh

# 开发端口
CMD 22

# 设置启动命令
CMD	["/run.sh"]
```

4. 创建镜像

```bash
# 当前路径 sshd_ubuntu
docker build -t sshd:dockerfile .
```
 5. 测试运行

```bash
# 运行容器
docker run -d -p 10122:22 sshd:dockerfile
# 打开一个终端
ssh root@localhost -p 10122
```
