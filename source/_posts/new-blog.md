---
layout: ‘n
title: "git 操作"
date: 2017-09-04 13:34:03
tags: [编程]
categories: [编程]
---

1.git 的一些命令


<h4>初始化git</h4>
{% codeblock %}
	git init
{% endcodeblock %}

<h4>将项目的所有文件添加到仓库</h4>
{% codeblock %}
	git add .
{% endcodeblock %}

<h4>将add的文件添加注释并commit到仓库</h4>
{% codeblock %}
	git commit -m "注释语句"
{% endcodeblock %}

<h4>将本地的库关联到github上,这里的地址是https</h4>
{% codeblock %}
	git remote add origin https://github.com/Hzert/myhexo.git  
{% endcodeblock %}

<h4>上传github之前要先pull一下</h4>
{% codeblock %}
	git pull origin master  
{% endcodeblock %}

<h4>上传代码到github</h4>
{% codeblock %}
	git push -u origin master 
{% endcodeblock %}

<h4>还有一些其他的操作</h4>
比如你想查看仓库的状态
{% codeblock %}
	git status 
{% endcodeblock %}
查看提交日志
{% codeblock %}
	git log
{% endcodeblock %}

创建新分支，并且切换到新分支
{% codeblock %}
	git checkout -b dev
{% endcodeblock %}

查看当前分支
{% codeblock %}
	git branch
{% endcodeblock %}

提交到当前分支
{% codeblock %}
	git push origin dev
{% endcodeblock %}

合并到主分支，先切换到主分支，在merge
{% codeblock %}
	git checkout master
	git merge dev
{% endcodeblock %}

合并之后，还要push一次
{% codeblock %}
	git push origin master 
{% endcodeblock %}

删除分支
{% codeblock %}
	git branch -d dev
	git push origin :dev
{% endcodeblock %}

查看与github绑定的地址
{% codeblock %}
	git push -u origin master 
{% endcodeblock %}
1.将关联错误的远程库移除
{% codeblock %}
	git remote rm origin
{% endcodeblock %}
2.重新关联远程库
{% codeblock %}
	git remote add origin git@github.com/Hzert/myhexo.git
{% endcodeblock %}

一、远程仓库有master和dev分支
1. 克隆代码
git clone https://github.com/master-dev.git  
# 这个git路径是无效的，示例而已
2. 查看所有分支
git branch --all  
# 默认有了dev和master分支，所以会看到如下三个分支
# master[本地主分支] origin/master[远程主分支] origin/dev[远程开发分支]
# 新克隆下来的代码默认master和origin/master是关联的，也就是他们的代码保持同步
# 但是origin/dev分支在本地没有任何的关联，所以我们无法在那里开发
3. 创建本地关联origin/dev的分支
git checkout dev origin/dev  
# 创建本地分支dev，并且和远程origin/dev分支关联，本地dev分支的初始代码和远程的dev分支代码一样
4. 切换到dev分支进行开发
git checkout dev  # 这个是切换到dev分支，然后就是常规的开发
5. 为了更好的理解，最好继续看看下文。

二、假设远程仓库只有mater分支
1. 克隆代码
git clone https://github.com/master-dev.git  
# 这个git路径是无效的，示例而已
2. 查看所有分支
git branch --all  
# 默认只有master分支，所以会看到如下两个分支
# master[本地主分支] origin/master[远程主分支]
# 新克隆下来的代码默认master和origin/master是关联的，也就是他们的代码保持同步
3. 创建本地新的dev分支
git branch dev  # 创建本地分支
git branch  # 查看分支
# 这是会看到master和dev，而且master上会有一个星号
# 这个时候dev是一个本地分支，远程仓库不知道它的存在
# 本地分支可以不同步到远程仓库，我们可以在dev开发，然后merge到master，使用master同步代码，当然也可以同步
4. 发布dev分支
发布dev分支指的是同步dev分支的代码到远程服务器
git push origin dev:dev  # 这样远程仓库也有一个dev分支了
5. 在dev分支开发代码
git checkout dev  # 切换到dev分支进行开发
# 开发代码之后，我们有两个选择
# 第一个：如果功能开发完成了，可以合并主分支
git checkout master  # 切换到主分支
git merge dev  # 把dev分支的更改和master合并
git push  # 提交主分支代码远程
git checkout dev  # 切换到dev远程分支
git push  # 提交dev分支到远程
# 第二个：如果功能没有完成，可以直接推送
git push  # 提交到dev远程分支
# 注意：在分支切换之前最好先commit全部的改变，除非你真的知道自己在做什么
6. 删除分支
git push origin :dev  # 删除远程dev分支，危险命令哦
# 下面两条是删除本地分支
git checkout master  # 切换到master分支
git branch -d dev  # 删除本地dev分支

-别的资源：http://www.jianshu.com/p/5dfa49a97ce8

##配置用户名和邮箱
{%codeblock%}
git config --global user.name "用户名"
git config --global user.email "邮箱地址"
{%endcodeblock%}

## 重点！！ git 修改远程仓库地址
方法有三种：
1.修改命令
{%codeblock%}
git remote origin set-url [url]
{%endcodeblock%}
2.先删后加
{%codeblock%}
git remote rm origin
git remote add origin [url]
{%endcodeblock%}
3.直接修改config文件

