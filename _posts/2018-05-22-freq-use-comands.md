---
layout: article
title: 常用工程命令
tags: 编程
key: code2
category: 编程
date: 2018-05-22 10:00:00
modify_date: 2019-01-11 17:45:00
---

总结一些常用的工程命令用法。

<!--more-->

## git

- `git clone ...`：从...克隆仓库
- `git add <filename>`：将本地的...加入到暂存区
- `git commit -m "..."`：将暂存区的改动提交到HEAD
- `git push origin master`：将改动提交到远端仓库，可以把 *master* 换成你想要推送的任何分支。 
- `git branch`：查看仓库的分支
- `git checkout branchname`：切换分支

## SSH

- `scp 文件名/-r 文件夹名 服务器账号：路径`：将文件拷贝到服务器，自动覆盖同名文件

