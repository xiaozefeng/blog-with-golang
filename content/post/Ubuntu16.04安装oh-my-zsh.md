---
title: "Ubuntu16安装oh-my-zsh"
date: 2018-06-13T21:44:36+08:00
draft: true
tags: ["Ubuntu"]
---

<!--more-->
## 安装 zsh
```bash
sudo apt-get update
apt-get install zsh
```

## 下载安装 oh-my-zsh
```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## 将默认的shell改为zsh
```bash
chsh -s /bin/zsh
```

## 安装zsh-autosuggestions插件
[GitHub - zsh-users/zsh-autosuggestions: Fish-like autosuggestions for zsh](https://github.com/zsh-users/zsh-autosuggestions)

```bash
# clone
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# Add the plugin to the list of plugins for Oh My Zsh to load:
plugins=(zsh-autosuggestions)
```
