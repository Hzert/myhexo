---
title: css
date: 2017-09-07 15:39:53
tags: [css]
categories: [编程]
---


## 百度百科这样介绍 css :
	层叠样式表(英文全称：Cascading Style Sheets)
		是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）
		等文件样式的计算机语言。
		CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。

## [菜鸟教程](http://www.runoob.com/css/css-intro.html)里面这么介绍：
	什么是 CSS?
		*  CSS 指层叠样式表 (Cascading Style Sheets)
		*  样式定义如何显示 HTML 元素
		*  样式通常存储在样式表中
		*  把样式添加到 HTML 4.0 中，是为了解决内容与表现分离的问题
		*  外部样式表可以极大提高工作效率
		*  外部样式表通常存储在 CSS 文件中
		*  多个样式定义可层叠为一

{% codeblock %}
	body{
		font-size:75%;
		font-family:verdana,arial,'sans serif';
		background-color:#FFFFF0;
		color:#000080;
		margin:10px;
	}

	h1 {font-size:200%;}
	h2 {font-size:140%;}
	h3 {font-size:110%;}

	th {background-color:#ADD8E6;}

	ul {list-style:circle;}
	ol {list-style:upper-roman;}

	a:link {color:#000080;}
	a:hover {color:red;}<
{% endcodeblock %}

## 引用方法：
{% codeblock %}
	<link href="../css/index.css" type="text/css">
{% endcodeblock %}