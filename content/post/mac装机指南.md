---
title: "Mac装机指南"
date: 2018-06-13T21:42:10+08:00
draft: true
---

<!--more-->
## 安装包管理工具 HomeBrew
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
## brew 配置
### 替换成中科大学源
```bash
替换brew.git:
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

替换homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```
## 替换 Homebrew Bottles源
```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
source ~/.zshrc
```

### 还原HomeBrew配置 `Homebrew Bottles 注释掉HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles`
```bash
重置brew.git:
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git

重置homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git

```


### brew cask 安装
```bash
brew cask
```

### 预览软件安装
```bash
 brew cask install qlcolorcode &&
 brew cask install qlstephen  &&\\
 brew cask install qlmarkdown &&\\
 brew cask install quicklook-json &&\\
 brew cask install qlprettypatch &&\\
 brew cask install quicklook-csv &&\\
```
### Java安装
[Java SE Development Kit 8 - Downloads](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

### 命令行软件安装
```bash
brew update  && brew upgrade \\
&& brew install git \\
&& brew install go\\
&& brew install tree\\
&& brew install node \\
&& brew install ruby\\
&& brew install python3\\
&& brew install mycli\\
&& brew install maven\\
&& brew install gradle\\
&& brew install cmake\\
&& brew install redis\\
&& brew install httpd\\
&& brew install jmeter\\
&& brew install siege\\
&& brew install subversion\\
&& brew install tmux\\
&& brew install vim\\
&& brew install zsh-autosuggestions\\
&& brew install mysql\\
```

## 图形化界面软件
```bash
 brew cask install alfred
 brew cask install appcleaner
 brew cask install cheatsheet
 brew cask install google-chrome
 brew cask install onepassword
 brew cask install sublime-text
 brew cask install totalfinder
 brew cask install the-unarchiver
 brew cask install appcleaner
 brew cask install aria2gui
 brew cask install youdaodict
 brew cask install macvim
 brew cask install jd-gui
 brew cask install sequel-pro
 brew cask install foxmail
 brew cask install dropbox 
```


## 配置Dropbox
![](http://7xv4mv.com1.z0.glb.clouddn.com/2018-04-17-073322.png)

## 配置Docker
- 打开Docker->Preferences...
- Insecure registries配置:registry.mirrors.aliyuncs.com
- Registry mirrors配置刚刚专属地址那里自己的镜像加速器地址即可. (https://2dipklk7.mirror.aliyuncs.com)

## item2 安装与配置
[iterm2下载页面](https://www.iterm2.com/downloads.html)

### 基本配置
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fqehp9soi9j30m40ep77u.jpg)
![](http://7xv4mv.com1.z0.glb.clouddn.com/2018-04-16-064052.png)

### powerline 字体安装
```bash
# 下载
git clone https://github.com/powerline/fonts.git
# 安装
cd fonts
./install.sh
# 删除安装包
cd ..
rm -rf fonts
```

## ipic 下载与配置7牛云图床
资源: xiaozefeng
Access Key: VrIXYo8pG5Joe61bkFZD56Gb9SER4gBwShq1y_YK
Secret Key: MWZxZ9TSOCyXojn-G9P8zkbKsnboRG4Ml5V9HrkM
网址前缀: http://7xv4mv.com1.z0.glb.clouddn.com


## 软件安装列表
1. [Mac App Store 上的“截图(Jietu)-快速标注、便捷分享的截屏工具”](https://itunes.apple.com/cn/app/%E6%88%AA%E5%9B%BE-jietu-%E5%BF%AB%E9%80%9F%E6%A0%87%E6%B3%A8-%E4%BE%BF%E6%8D%B7%E5%88%86%E4%BA%AB%E7%9A%84%E6%88%AA%E5%B1%8F%E5%B7%A5%E5%85%B7/id1059334054?mt=12)
2. [Releases · fikovnik/ShiftIt · GitHub](https://github.com/fikovnik/ShiftIt/releases)
3. [Documentation for Visual Studio Code](https://code.visualstudio.com/docs/?dv=osx)
4. bartender
5. cornerstone
6. idea
7. postman
8. pdf export
9. visual studio code
10. SnippetsLab
11. [Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
12. [Welcome to f.lux for macOS](https://justgetflux.com/news/pages/macquickstart/)
13. flux
14. rdm
15. 印象笔记
16. [macOS版TeamViewer下载](https://www.teamviewer.com/zhcn/download/mac/)
17. [Transmit 5.1.1 一款功能齐全的FTP客户端 - 精品MAC应用分享](http://xclient.info/s/transmit.html?t=b9f2c41fb9dbdc423533bc52178734bae89bcf94#versions)
18. [SnippetsLab 1.7.4 构建你的私人代码片段库 - 精品MAC应用分享](http://xclient.info/s/snippetslab.html?t=b9f2c41fb9dbdc423533bc52178734bae89bcf94#versions)
19. [Download Postman](https://app.getpostman.com/app/download/osx64?utm_source=site&utm_medium=apps&utm_campaign=macapp&_ga=2.54396268.536085204.1523966954-325928436.1523966954)
20. [Install Docker for Mac | Docker Documentation](https://docs.docker.com/docker-for-mac/install/#download-docker-for-mac)
  
