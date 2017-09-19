---
layout: ‘n
title: "star"
date: 2017-09-07 13:34:03
tags: [生活,hexo]
categories: 生活
---

这是第一次弄博客,基本的一些配置，主题。全是百度，加自己的一些摸索出来的。纯小白一个！
	建这个博客，主要是因为笔记问题，另外是有逼格。

跌跌撞撞选择一款非常简单的主题。然后里面一些东西都还没有弄明天。因为我刚从ejs那边逃离，现	在这个主题又是用jade。所以导致自己很是困惑。有很多东西，会慢慢的开始添加，我得花时间好	好去弄弄了

插入代码快：
	
{% codeblock %}
	console.log("这是代码块")
{% endcodeblock %}

重要的引述：
{% pullquote %}
		重要的引述content
{% endpullquote %}

插入图片：
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}

link：
{% link text url [external] [title] %}

其他文章链接：
{% post_path slug %}
dada
{% post_link slug [title] %}

{% img [class names] ../img/01.jpg [width] [height] [title text [alt text]] %}
{% link 百度一下 http://www.baidu.com [这是什么] [超链接] %}
{% jsfiddle AntBody/138zf8kk js,html,css,result dark %}
{% iframe http://v.youku.com/v_show/id_... 930 542 %}