---
title: webpack vue-cli安装 mac vue-cli安装
date: 2017-09-22 17:02:45
tags: [vue]
categories: [编程]
---
### 安装

1.我们将会使用webpack去为我们的模块打包，预处理，热加载。如果你对webpack不熟悉，它就是可以帮助我们把多个js文件打包为1个入口文件，并且可以达到按需加载。这就意味着，我们不用担心由于使用太多的组件，导致了过多的HTTP请求，这是非常有益于产品体验的。但我们并不只是为了这个而使用webpack，我们需要用webpack去编译.vue文件，如果没有使用一个loader去转换我们.vue文件里的style、js和html，那么浏览器就无法识别。

2.模块热加载是webpack的一个非常碉堡的特性，将会为我们的单页应用带来极大的便利。
通常来说，当我们修改了代码刷新页面，那应用里的所有状态就都没有了。这对于开发一个单页应用来说是非常痛苦的，因为需要重新在跑一遍流程。如果有模块热加载，当你修改了代码，你的代码会直接修改，页面并不会刷新，所以状态也会被保留。
3.Vue也为我们提供了CSS预处理，所以我们可以选择在.vue文件里写LESS或者SASS去代替原生CSS。
4.我们过去通常需要使用npm下载一堆的依赖，但是现在我们可以选择Vue-cli。这是一个vue生态系统中一个伟大创举。这意味着我们不需要手动构建我们的项目，而它就可以很快地为我们生成。
首先，安装vue-cli。(确保你有node和npm)
{%codeblock%}
npm i -g vue-cli
{%endcodeblock%}
然后创建一个webpack项目并且下载依赖
{%codeblock%}
vue init webpack vue-time-tracker
cd vue-time-tracker
npm i
{%endcodeblock%}
接着使用 npm run dev 在热加载中运行我们的应用
这一行命令代表着它会去找到package.json的scripts对象，执行node bulid/dev-server.js。在这文件里，配置了Webpack，会让它去编译项目文件，并且运行服务器，我们在localhost:8080即可查看我们的应用。


### mac 安装vue-cli

{%codeblock%}
npm install vue-cli -g

vue //查看是否安装成功

vue init webpack-simple demo //新建vue项目demo名随便取
然后依次输入项目名，描述等
切换到项目下安装依赖
npm install
npm run dev    //运行项目
{%endcodeblock%}

 
链接：http://www.imooc.com/article/details/id/6991
