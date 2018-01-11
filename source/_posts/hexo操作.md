---
title: hexo简单操作
date: 2017-09-18 13:13:56
tags: [hexo]
categories: [编程]
---

### hexo官网
   https://hexo.io/zh-CN/

1.安装Hexo
{%codeblock%}
    npm install -g hexo 
{%endcodeblock%}

2.进入工作目录，进行初始化
{%codeblock%}
    cd 工作目录
    hexo init
{%endcodeblock%}

3.安装依赖包
{%codeblock%}
    npm install
{%endcodeblock%}

4.运行
{%codeblock%}
    hexo server
{%endcodeblock%}

默认本地地址是localhost:4000

### github发布
1.创建github账户，假设账户为XXX
2.创建仓库，仓库的名称必须要注意：xxxx.github.io.其中xxx为账户名
3.设置SSH keys:需要在gitbash下输入如下命令
{%codeblock%}
查找是否存在SSH Keys
ls -al ~/.ssh
如果是windows下，文件的地址应该在C:/用户/.ssh下
生成KEY命令
ssh-agent -s
ssh-add ~/.ssh/id_rsa
如果这里出现错误,请执行下面的命令
eval 'ssh-agent -s'
ssh-add
{%endcodeblock%}
4.复制粘贴id_rsa.pub文件中的内容到github中设置SSH key.最后使用如下命令完成测试
{%codeblock%}
ssh -T [git@github.com](mailto:git@github.com)
{%endcodeblock%}

### hexo的操作命令
简单的操作方法：
{%codeblock%}
    hexo n == hexo new        增加新文章
    hexo g == hexo generate   生成静态文件
    hexo s == hexo server     启动服务
    hexo d == hexo deploy     部署
    hexo s --debug            调试模式


    
文件头格式：
title: ##文章标题
date: ##时间，格式为 YYYY-MM-DD HH:mm:ss
categories: ##分类
tags: ##标签，多标签格式为 [tag1,tag2,...]
keywords: ##文章关键词，多关键词格式为 keyword1,keywords2,...
description: ##文章描述
---
正文
{%endcodeblock%}
## 列如：
{%codeblock%}
title: 这是一篇测试文章
date: 2015-03-21 15:13:48
categories: Hexo
tags: [Hexo,测试]
keywords: Hexo,文章,测试
description: 这是一篇测试文章，用于测试Hexo文章文件头。
---
正文
{%endcodeblock%}

## 在本地资料丢失后  在其他电脑上修改博客 可以使用以下步骤：
1. 使用git clone git@github.com:CrazyMilk/CrazyMilk.github.io.git拷贝仓库（默认分支为hexo）；
2. 在本地新拷贝的http://CrazyMilk.github.io文件夹下通过Git bash依次执行下列指令：npm install hexo、npm install、npm install hexo-deployer-git（记得，不需要hexo init这条指令）


## md语法
[dsda](https://www.baidu.com)
 1. 链接文字用［］表示 也可以表示图片
 2. ～～请删除我把～～   ～～删除
 3. 字体加粗 ＊＊加粗＊＊  **加粗**
 
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86   
    src="http://music.163.com/outchain/player?type=2&id=25706282&auto=0&height=66">  
</iframe> 