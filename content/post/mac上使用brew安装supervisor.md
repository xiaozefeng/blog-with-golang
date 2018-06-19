---
title: "Mac上使用brew安装supervisor"
date: 2018-06-13T21:41:20+08:00
draft: true
---

<!--more-->
```bash
# 安装
brew install supervisor

# 启动
supervisorctl -c /usr/local/etc/supervisord.ini
# 配置app
# 创建目录
mkdir -p /usr/local/etc/supervisor.d
# 创建 app.ini
[program:logstash]
directory = /Users/hylexus/app/logstash-5.2.0/bin
command = /Users/hylexus/app/logstash-5.2.0/bin/logstash -f /Users/hylexus/app/logstash-5.2.0/my-task/echo.conf -l /Users/hylexus/app/logstash-5.2.0/logs/test-logstash.log
autostart = false
startsecs = 5
autorestart = true
startretries = 3
user = hylexus
redirect_stderr = true
stdout_logfile_backups = 20
stdout_logfile=/usr/local/var/log/logstash.log
stdout_logfile_maxbytes=10MB
stderr_logfile=/usr/local/var/log/logstash-err.log
stderr_logfile_maxbytes=10MB

```
