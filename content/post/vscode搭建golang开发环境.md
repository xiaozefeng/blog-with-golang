---
title: "vscode搭建golang开发环境"
date: 2018-06-13T21:46:56+08:00
draft: true
---

<!--more-->

## 安装go
```bash
brew install go
# 验证
go env
```

## 安装 vscode
[Visual Studio Code - Code Editing. Redefined](https://code.visualstudio.com/)


## vscode安装go插件
在插件中搜索go安装即可

## vscode 配置go
cmd + , 打开用户设置, 输入以下

```json
"files.autoSave": "onFocusChange",
"go.buildOnSave": true,
"go.lintOnSave": true,
"go.vetOnSave": true,
"go.buildFlags": [],
"go.lintFlags": [],
"go.vetFlags": [],
"go.useCodeSnippetsOnFunctionSuggest": false,
"go.formatOnSave": false,
"go.formatTool": "goreturns",
"go.goroot": "你的gooroot",
"go.gopath": "你的gopath"
```

## 安装插件 ,请参考 go get 如何设置代理
```bash
go get -u -v github.com/nsf/gocode
go get -u -v github.com/rogpeppe/godef
go get -u -v github.com/golang/lint/golint
go get -u -v github.com/lukehoban/go-outline
go get -u -v sourcegraph.com/sqs/goreturns
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v github.com/tpng/gopkgs
go get -u -v github.com/newhook/go-symbols
go get -u -v golang.org/x/tools/cmd/guru
```

