---
title: "Ubuntu16中文乱码问题"
date: 2018-06-13T21:45:07+08:00
draft: true
---

<!--more-->
# Ubuntu16.04 中文乱码问题
```bash
# 编辑
vim /etc/default/locale

LANGUAGE="zh_CN:en_US:en"
LC_CTYPE="en_US.UTF-8"
LC_ALL="en_US.UTF-8"
LANG="en_US.UTF-8"
# 验证
locale
```
