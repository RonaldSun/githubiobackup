---
layout: article
title: 常用工程命令
tags: 编程
key: code2
category: 编程
date: 2018-05-22 10:00:00
modify_date: 2021-06-15 14:55:00
---

总结一些常用的工程命令用法。

<!--more-->

## git

- `git clone ...`：从...克隆仓库

- `git add <filename>`：将本地的...加入到暂存区

- `git commit -m "..."`：将暂存区的改动提交到HEAD

- `git push origin master`：将改动提交到远端仓库，可以把 *master* 换成你想要推送的任何分支。 

- `git branch`：查看仓库的分支， `git branch name`：新建name分支

- `git checkout branchname`：切换分支，`git checkout <filename>`： 将文件还原到最近一次commit或add的状态

- `git merge --strategy=ours master` : 将master分支merge到当前分支, 用当前分支解决所有conflit

- 回退：

  先查看提交日志：

  ```bash
  git log
  ```

  本地回退：

  ```bash
  git reset --hard commit_id(commit字符)
  ```

  将远程库同步

  ```bash
  git push origin HEAD --force
  ```

- 撤销add或commit:  ```git reset HEAD~1```

- `git pull `=`git fetch`+`git merge`

## SSH

- `scp 文件名/-r 文件夹名 服务器账号：路径`：将文件拷贝到服务器，自动覆盖同名文件

## docker
- 基础教程: http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html
- 删除所有停止容器： `docker rm $(sudo docker ps -a -q)`
- 运行docker: `docker exec -ti 430f758bb83c bash`

## ubuntu操作
- `du -h --max-depth=1` : 查看文件大小


## profiler
- py-spy: `py-spy record -s -F -n -p 9396 -o profile.svg`

## debug
- `gdb --ex=r --args python mm_benchmark.py`
- `l` :显示代码 `p`: print

## ros
- 找pkg: https://answers.ros.org/question/288501/ros2-equivalent-of-rospackagegetpath/