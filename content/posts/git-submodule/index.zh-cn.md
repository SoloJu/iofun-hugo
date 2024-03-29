---
title: 'Git submodule的使用'
date: 2024-01-31T22:56:29+08:00
lastmod: 2024-01-31T22:56:29+08:00
draft: false
author: "Will"
authorLink: ""
description: "Git Submodule 的建立和移除"
images: []
resources:
- name: "featured-image"
  src: "featured-image.jpg"

tags: ["installation", "configuration"]
categories: ["documentation"]

lightgallery: true

toc:
  auto: false
---

关于Git Submodule 的建立和移除

<!--more-->

## 1 Git Submodule 是什么

项目中经常使用别人维护的模块，在git中使用子模块的功能能够大大提高开发效率。

使用子模块后，不必负责子模块的维护，只需要在必要的时候同步更新子模块即可。

## 2 子模块的添加
添加子模块非常简单，命令如下：
```bash
git submodule add <url> <path>
```
其中，url为子模块的路径，path为该子模块存储的目录路径。

执行成功后，git status会看到项目中修改了.gitmodules，并增加了一个新文件（为刚刚添加的路径）

## 3 子模块的使用
克隆项目后，默认子模块目录下无任何内容。需要在项目根目录执行如下命令完成子模块的下载：
```bash
git submodule init
git submodule update
```
执行后，子模块目录下就有了源码，再执行相应的makefile即可。

## 4 子模块的更新
子模块的维护者提交了更新后，使用子模块的项目必须手动更新才能包含最新的提交。

在项目中，进入到子模块目录下，执行 `git pull` 更新，查看`git log`查看相应提交。

完成后返回到项目目录，可以看到子模块有待提交的更新，使用`git add`，提交即可。

## 5 删除子模块
有时子模块的项目维护地址发生了变化，或者需要替换子模块，就需要删除原有的子模块。

删除子模块较复杂，步骤如下：

`rm -rf` 子模块目录 删除子模块目录及源码

`vim .gitmodules` 删除项目目录下.gitmodules文件中子模块相关条目

`vim .git/config` 删除配置项中子模块相关条目

`rm .git/module/*` 删除模块下的子模块目录，每个子模块对应一个目录，注意只删除对应的子模块目录即可
