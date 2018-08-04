---
title: angular-2
date: 2018-04-26 21:42:53
tags: [angular]
categories: [angular]
---
## angular 的数据绑定采用什么机制？

`脏检查机制`

双向数据绑定是AngularJS的核心机制之一。当view中有任何数据变化时，会更新到model,但model中数据有变化时，view也会同步更新,显然，这需要一个监控。

原理就是,Angular在scope模型上设置了一个监听队列，用来监听数据变化并更新view，每次绑定一个东西到 view 上时 AngularJS 就会往 $watch 队列里插入一条 $watch，用来检测它监视的 model 里是否有变化的东西。当浏览器接收到可以被 angular context 处理的事件时，$digest 循环就会触发，遍历所有的 $watch，最后更新 dom

举个例子
{%codeblock%}
<button ng-click="val=val+1"></button>
{%endcodeblock%}

click时会产生一次更新的操作（至少触发两次$digest循环）

- 按下按钮
- 浏览器接收到一个事件，进入到angular context
- $digest 循环开始执行，查询每个$watch是否变化
- 由于监视 $scope.val 的 $watch 报告了变化，因此强制再执行一次 $digest 
- 新的 $digest 循环未检测到变化
- 浏览器拿回控制器，更新 $scope.val 新值对应的 dom

`$digest 循环的上限是 10 次（超过 10次后抛出一个异常，防止无限循环）。`


## 详述 angular 的 “依赖注入”

依赖注入是一种软件设计模式，目的是处理代码之间的依赖关系，减少组件间的耦合。

AngularJS 是通过构造函数的参数名字来推断依赖服务名称的，通过 toString() 来找到这个定义的 function 对应的字符串，然后用正则解析出其中的参数（依赖项），再去依赖映射中取到对应的依赖，实例化之后传入

{%codeblock%}
function myCtrl = ($scope, $http){
    $http.get('/api/animals').success(function(data){
        $scope.animals = data;
    })
}
{%endcodeblock%}

`也就是说，在 Angular App 运行的时候，调用 myCtrl，自动做了 $scope 和 $http 两个依赖性的注入。`

数组注释法
{%codeblock%}
myApp.controller('myCtrl', ['$scope', '$http', function($scope, $http){
    ...
}])
{%endcodeblock%}