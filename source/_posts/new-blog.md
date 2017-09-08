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



-别的资源：http://www.jianshu.com/p/5dfa49a97ce8