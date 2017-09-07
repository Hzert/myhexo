---
layout: ‘n
title: "Hexo Docs基本用法"
date: 2017-09-04 13:34:03
tags:[生活]
---



这部分Docs分了8块内容，分别从写作、前置声明、标签插件、资源目录、数据文件、服务器、生成器、部署。也许翻译得不得当，但是我尽量把主要内容呈现出来并加上自己的理解。

写作

写作之前当然得先创建一个.md文件，使用命令 hexo new [layout] <title> ，其中layout默认为post，前面提过。

Layout布局
<!-- more -->
Hexo提供了3种默认的布局， post 、 page 和 draft ，路径分别为： source/_posts 、 source 、 source/_draft 。如果你将在文章前置申明中，将layout设置为false，那么这篇文章将不会有任何的布局。

Filename文件名

Hexo会默认将文章的标题当做文件名，但是你可以编辑 _config.yml 配置文件中的 new_post_name 来改变默认的文件名。
例如：使用 hexo new hello 命令创建一篇为hello文章，Hexo会默认在_posts目录下给你创建一个名为hello.md的文件。假如你将 new_post_name 改为了 :year-:month-:day-:title.md ，那么hexo就自动帮你创建名为2015-05-16-hello.md（当前日期为2015年5月16）

:title 文章标题
:year 创建年份
:month 月份，如4月为 04
:day 日期
i_month 月份，单数字，比如4月就是 4
i_day 日期，单数字
Drafts草稿

Hexo提供草稿功能，在 _drafts 目录下的文章不会发表到网站上，你可以通过命令 hexo publish [layout] <title> 发布你的草稿，改命令会将文章移到 _posts 目录下。但是也可以设置 _config.yml 配置文件的 render_drafts 字段，使草稿默认发布到站点中。

Scaffolds模版

当你使用 new 命令创建一篇文章的时候，Hexo会根据scaffolds目录中的模版帮你生成文章。假如执行 hexo new photo "My Gallery" ，Hexo会尝试在scaffolds目录中去寻找photo.md的模版文件，然后基于它创建标题为My Gallery的文章。
它的用处就是能够在模版中写入你某一类文章都要添加的共同内容，这样你基于模版创建文章的时候，就不用再重复写入那部分内容。

前置申明

顾名思义，就是写在文章前面的一块内容，为了对文章进行某些设置。它有两种书写方式：

YAML方式，以三短线结束

title: Hello World
date: 2013/7/13 20:46:25

JSON方式，以三分号结束

"title": "Hello World",
"date": "2013/7/13 20:46:25"
;;;
参数列表

layout: 布局，一般不用写，默认就行
title: 标题，这个必须要有
date: 时间
updated: 修改时间
comments: 是否开启评论，默认为true
tags: 文章标签
categories: 文章分类
permalink: 文章永久链接，一般不用写，默认就行
在写标签和分类的时候，可能会有多个的情况，多个标签可以无序排列的方式书写，而分类可能会有多级分类的情况。如何书写举例如下:

categories: 
- Sports
- Baseball
tags:
- Injury
- Fight
- Shocking
标签插件

这里说的标签插件不同于文章中的标签，它可以帮助你在文章中快速嵌入一些特殊的内容。

Block Quote-块引用

插入带有作者信息的应用，体现在Html上就是在 blockquote 标签下加入了 footer 标签。但是会给文章带来不一样的显示效果，书写格式非常简单。

{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
看下面的例子就大概知道怎么书写了，第一种最简单的方式就等于markdown里的 > 语句。

{% blockquote %}
I love you forever
{% endblockquote %}

{% blockquote pengloo53 http://www.linux2me.com %}
I love you forever 我爱你
{% endblockquote %}

{% blockquote David Levithan, Wide Awake %}
I love you forever
{% endblockquote %}
显示效果为（主题为 light-ch ）：


显示效果
Code Block代码块

在文章中插入代码块可以使用下面方式书写

{% codeblock [title] [lang:language] [url] [link text] %}
code snippet
{% endcodeblock %}
实例如下


code block 实例

显示效果


显示效果
Pull Quote

这个插件可以帮助您在文章中插入重要引述

{% pullquote [class] %}
content
{% endpullquote %}
jsFiddle

在文章中嵌入jsFiddle片段。

{% jsfiddle shorttag [tabs] [skin] [width] [height] %}
Gist

嵌入Gist片段

{% gist gist_id [filename] %}
iFrame

插入网页框架

{% iframe url [width] [height] %}
Image

插入图片，可以自定义大小

{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}
Link

插入带有target="_blank"属性值的链接。

{% link text url [external] [title] %}
Include Code

从资源目录中插入代码片段。

{% include_code [title] [lang:language] path/to/file %}
Youtube

在文章中插入Youtube视频。天朝的孩子就不用试了

{% youtube video_id %}
Vimeo

在文章中插入Vimeo视频。

{% vimeo video_id %}
Include Posts

包含其他文章的链接(这个我测试没有出现效果, 不知道是不是我的写法有问题, 希望有人可以测试一下)。

{% post_path slug %}
{% post_link slug [title] %}
Include Assets

包含文章资源。 (具体怎么使用，还不太明白，希望有人可以测试一下)

{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
Raw

一些内容不想被主题渲染，可以使用该插件呈现原始状态。

{% raw %}
content
{% endraw %}
资源目录

Assets指的是那些不在source目录下的资源，比如图片、CSS文件或者Javascript文件。Hexo提供一种更方便的方法来管理这些资源（Assets）。想使其生效，首先修改 post_asset_folder 字段的设置，将其值改为 true 。
当生效后，在你创建文章的时候，Hexo会创建一个同名目录，你可以将该文章关联的资源全部放到该目录下。这样就可以更加方便的使用它们了。
使用方法就是上面介绍过的标签插件。

{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
数据文件

有时，你可能会使用一些不在post中的模版数据，或者你想复用这些数据，那么你可以试用一下Hexo3中的『Data files』功能。这个特性加载source/_data目录中的YAML或者JSON文件，从而用到你的网站中。

例如，在source/_data目录中添加 menu.yml 文件。内容如下：

Home: /
Gallery: /gallery/
Archives: /archives/
在模版中，你可以这样使用它。

{% for link in site.data.menu %}
  <a href="{{ link }}">{{ loop.key }}</a>
{% endfor %}
服务器

Hexo server

在Hexo3中，服务器模块从主模块中分开了，你可以通过安装 hexo-server 来使用它。

npm install hexo-server --save
安装完成后，通过运行命令 hexo server 来启动本地服务。可以通过 http://localhost:4000 或者 http://0.0.0.0:4000 来访问你的网站。服务启动后，Hexo会监视文件的改动情况并且自动更新，也就是说你修改网站内容后不必重启服务器就可以见到效果。
如果你想修改端口，可以通过

hexo server -p 5000
命令来指定端口。

hexo server -s 启动静态模式，在静态模式中，只有public文件夹下的文件才会被放到服务器上，并且文件监听功能关闭。你可以在运行 hexo g 命令后运行该命令，通常用于生产系统中。

hexo server -i 192.168.1.1 指定IP访问，可以替代默认的 0.0.0.0 .

Pow

Pow是Mac上一个零配置的服务架构。通过 curl get.pow.cx | sh 命令下载并安装该软件；然后链接到项目文件夹中，步骤如下：

cd ~/.pow
ln -s /path/to/myapp index
通过上面命令，会在~/.pow目录下创建一个index的链接文件指向你的hexo根目录，然后你就可以通过访问 http://index.dev 就可以看到你的主页了。

生成器

这个很简单， hexo generate 一条命令生成静态站点。可以使用缩写 hexo g ，还可以显示你修改的文件并且重新生成，使用命令 hexo g --watch ，还用两种用法可以跟部署结合起来， hexo g -d or hexo d -g ，指的是生成后马上部署站点。

部署

部署的方式有多种，这里我主要介绍一下Git的方式，因为GitHub提供Pages功能，可以直接将站点部署到Github上。

主要就是设置 _config.yml 配置文件，

deploy:
    type: git
    repo: 这里是自己的SSH或者Https路径
    branch: master
这样就设置好了，注意将repo改成自己的。其他方式类似。部署命令很简单， hexo d 就OK了。

作者：jicemoon
链接：http://www.jianshu.com/p/e20deec143b1
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
作者：jicemoon
链接：http://www.jianshu.com/p/e20deec143b1
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。