---
layout: ‘n
title: "git 操作"
date: 2017-09-04 13:34:03
tags:
---
一、clone Repository
clone Github 上的Repository，如下： git clone git@github.com:FBing/design-patterns.git
二、管理分支
1、查看本地分支

<!--more-->
使用 Git branch命令，如下：
$ git branch
* master
*标识的是你当前所在的分支。
2、查看远程分支
命令如下：
git branch -r
3、查看所有分支
命令如下：
git branch -a
2、本地创建新的分支
命令如下：
git branch [branch name]
例如：
git branch gh-dev
3、切换到新的分支
命令如下：
git checkout [branch name]
例如：
Ricky@DESKTOP-1QPASTR MINGW64 /f/Git_Studio/design-patterns (master)
$ git checkout gh-dev
Switched to branch 'gh-dev'
Ricky@DESKTOP-1QPASTR MINGW64 /f/Git_Studio/design-patterns (gh-dev)
4、创建+切换分支
创建分支的同时切换到该分支上，命令如下：
git checkout -b [branch name]
git checkout -b [branch name] 的效果相当于以下两步操作：
git branch [branch name]
git checkout [branch name]
5、将新分支推送到github
命令如下：
git push origin [branch name]
例如：
git push origin gh-dev
6、删除本地分支
命令如下：
git branch -d [branch name]
例如：
git branch -d gh-dev
7、删除github远程分支
命令如下：
git push origin :[branch name]
分支名前的冒号代表删除。
例如：
git push origin :gh-dev