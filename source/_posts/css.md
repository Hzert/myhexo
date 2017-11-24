---
title: css
date: 2017-09-07 15:39:53
tags: [css,前端]
categories: [编程,css]
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

{% codeblock %}
	<style>
		body{
			margin:0;
			padding:0;
			font-size:14px;
		}
	</style>
{% endcodeblock %}
{% codeblock %}
	<div class="box" style="width:300px;height:300px"></div>
{% endcodeblock %}

## 选择器：
	一般的css选择器用得最多的是class，id这两种
		当然还有很多的选择器
		选择器有优先级前后 
{% codeblock %}
	id>class  important>id>class  imgportant>行内样式>id>class
{% endcodeblock %}

### 罗列一下，经常用的选择器

## 1. id
{% codeblock %}
	<style>
		#box{
			width:100px;
			height:100px;
			border:1px solid red;
		}
	</style>


	<div id="box"></div>
id选择页面内独有，class可以重复，当你有些地方的样式是一样的时候，可以选择class选择器，这样可以省很多代码。让自己的代码看起来简洁，清晰
{% endcodeblock %}

## 2. class
{% codeblock %}
	<style>
		.box{
			width:100px;
			height:100px;
			border:1px solid red;
		}
	</style>


	<div class="box"></div>
	<div class="box"></div>
{% endcodeblock %}

## 3. X(标签选择器)
{% codeblock %}
	a{
		text-decoration:none;
	}
{% endcodeblock %}
	如果想让页面上所有指定标签的样式改变，可以直接使用标签选择器

## 4. x,y(分组选择器)
在样式表具有相同样式的元素，就可以把所有元素组合在一起，用逗号分隔
{% codeblock %}
	h1,h2,h3,h4,h5,p{
		color:red;
	}
{% endcodeblock %}

## 5.x y（后代选择器）
选择指定元素内部的所有子元素以及后代元素
{% codeblock %}
	div a{
		text-decoration:none;
	}
	选择div下所有的a元素

	#box a{
		text-decoration:none;
	}
	选择id为box的元素下的所有a元素
{% endcodeblock %}

## 6.x>y(子元素选择器)
选择指定父元素的所有直接子元素。不包括孙元素等
{% codeblock %}
	div > ul{
		border:1px solid black;
	}

	x y 和x>y的区别 前者用于元素的所有后代元素，后者只作用于指定的第一代后代
{% endcodeblock %}

## 7.伪类选择器 
#### 1. :link 选择所有未访问的链接
#### 2. :visited 选择所有访问过的链接
#### 3. :active 用于选择活动的链接
#### 4. :target 用于选择当前活动的目标元素
#### 5. :hover 用于鼠标移入链接时添加的特殊样式。（用得最多）
{% codeblock %}
	div:hover{
		background:red;
	}
	a:hover{
		border:1px solid black;
	}
{% endcodeblock %}

#### 6. :before和:after  用于在指定元素周围生成一些内容
{% codeblock %}
	p:before{
		content:"看这里 - ";
		color:red;
		font-weight:bold;
	}
{% endcodeblock %}

:after 一般用来清除浮动
{% codeblock %}
	.clear-fix{
		overflow:hidden;
		zoom:1;
	}
	.clear-fix:after{
		content:"";
		width:0;
		clear:both;
	}
{% endcodeblock %}
:after :before 还有一些妙用
{% codeblock %}
	a {  
		position: relative;  
		display: inline-block;  
		outline: none;  
		text-decoration: none;  
		color: #000;  
		font-size: 32px;  
		padding: 5px 10px;  
	}  
		  
	a:hover::before, a:hover::after { position: absolute; }  
	a:hover::before { content: "\5B"; left: -20px; }  
	a:hover::after { content: "\5D"; right:  -20px; }
{% endcodeblock %}
这是一个hover效果，鼠标移到a元素上时会出现边框，还有很多效果可以实现
![出现边框](http://img1.cheny.org/dimblog/2013/10/6cc221614774e78add77d4e7a1171f591.gif)

### 7. :not(seletor)
css3的一个选择器。取反 除了指定元素以外的所有元素
{% codeblock %}
	p{
		color:red;
	}
	*:not(p){
		color:black;
	}
{% endcodeblock %}