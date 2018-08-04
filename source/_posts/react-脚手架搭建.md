---
title: react 脚手架搭建
date: 2018-03-13 17:44:44
tags: [react, 前端]
categories: [前端]
---
## react 用 create-react-app 脚手架搭建  

用法跟vue的差不多，似乎还简单一点

{%codeblock%}
npm install -g create-react-app

create-react-app my-app
cd my-app
npm start
{%endcodeblock%}

简单的几步，就能搭建出react项目

打开的是localhost:3000

打开package.json文件，会发现在dependencies里有三个依赖
{%codeblock%}
"react": "^16.2.0",
"react-dom": "^16.2.0",
"react-scripts": "1.1.1"
{%endcodeblock%}

然后呢，在scripts下还有一些命令，比如：start build之类的
{%codeblock%}
"start": "react-scripts start",
"build": "react-scripts build",
"test": "react-scripts test --env=jsdom",
"eject": "react-scripts eject"
{%endcodeblock%}

然后在node_modules文件夹下，就会发现有很多的依赖，有类似webpack-dev-server的--inline --hot自动刷新功能等等
看了这些，你会发现其实跟vue是相差不大的
