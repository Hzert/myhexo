---
title: angular
date: 2017-09-19 16:39:22
tags: [angular]
categories: [angular]
---
### 1.关于angularjs

哈哈，其实都可以自己百度到的，这里就不多说了。我们都是站在巨人的肩膀上。

### 2.获取AngularJs app的种子

对于像我一样的新手来说，初次着手angularjs时，肯定没有那个能力去自己去编写什么项目目录啊，文件啊之类的。所以我在github上找了一个种子。 
地址： https://github.com/glitchtank/angular-seed-master 
需要安装git，然后克隆到本地 
git clone https://github.com/glitchtank/angular-seed-master 
关于这个种子的介绍可以详细的阅读以下 README.md，这里就不多做介绍了，前端出身的同学肯定觉得我在说废话。

### 3.安装node，启动项目

nodejs下载地址：https://nodejs.org/en/download/ 根据自己的操作系统版本下载安装 
windows 进入cmd，进入到我们刚才clone的项目下，执行命令 node scripts/web-server.js 
然后在浏览器中输入 http://localhost:8000/app/index.html 可以看见一个简单的页面，自此项目启动成功。
![“图片描述”](/img/angular1.JPG) 


注意： 
1.关于端口8000，如果你的端口8000已经被其他程序占用，你可以在web-server.js中修改default_port，改成其他端口 . 
2.运行node scripts/web-server.js命令时，如果进入script再运行node web-server.js，浏览器中输入 http://localhost:8000/app/index.html 会报404.

### 4.认识整个项目
![“目录”](/img/angular2.jpg)
css文件夹下存放我们编写的一些css文件； 
img文件夹下存放我们需要用到的一些图片； 
js文件下： 
controller.js 控制器 
filter.js我们自己编写的一些过滤器 
service.js 调用后端api的连接一般放在这里

### 5.第一个小例子

该例子来自于《用angularjs开发下一代web应用》一书中的购物车例子。 
在项目下创建一个新的html页面：shopCart.html,内容如下
{%codeblock%}
<!DOCTYPE html>
<html ng-app="myApp">
<head lang="en">
    <meta charset="UTF-8">
    <title>购物车例子</title>
</head>
<body ng-controller="CartController">
<h1>your order</h1>
<div ng-repeat="item in items">
    <span>{{item.title}}</span>
    <input ng-model="item.count">
    <!--angularjs内置过滤器currency,实现美元格式化-->
    <span>"{{item.price}}"</span>
    <span>{{item.price*item.count}}</span>
</div>
<script src="lib/angular/angular.js"></script>
<script src="js/app.js"></script>
<script src="js/controllers.js"></script>
<script src="js/services.js"></script>
<script src="js/filters.js"></script>
<script src="js/directives.js"></script>
</body>
</html>
{%endcodeblock%}
在js/controller.js文件中添加

{%codeblock%}
function CartController($scope){
    $scope.items=[
        {tile:'pea',count:8,price:3.00},{tile:'apple',count:9,price:4.00}
    ]
}
{%endcodeblock%}

启动项目
{%codeblock%}
node scripts/web-server.js
{%endcodeblock%}


### Angular设置title信息解决SEO方面存在问题_AngularJS
Javascript框架在处理seo方面存在问题，因为爬虫在检索seo信息的时候会读不了js给其赋的值，导致搜索引擎收录不了或者收录了无效的信息,比如收录的可能是title={{title}}这样的，下面先说如何在路由跳转时修改页面的seo信息，现在spa跳转一般用route-ui了，就以这个为基础讲解，在app.js配置项state中加入title信息，如下：
{%codeblock%}
data:{ pageTitle:'user title'}
.state('index.user', {
    url: '/user',
    views: {
    'content@index': {
        templateUrl: 'templateHtml/user/user.html',
        controller: 'userCtrl'
    }
},
    data:{
        pageTitle:'user title'
    }
})
.state('index.user.a', {
    url: '/a',
    templateUrl: 'templateHtml/user/a.html',
    data:{
        pageTitle:'user a title'
    }
})
.state('index.user.b', {
    url: '/b',
    templateUrl: 'templateHtml/user/b.html',
    data:{
        pageTitle:'user b title'
    }
})
{%endcodeblock%}
然后使用通过监听$stateChangeSuccess来修改页面title:
{%codeblock%}
app.directive('title', ['$rootScope', '$timeout',
    function($rootScope, $timeout) {
        return {
            link: function() {
                var listener = function(event, toState) {
                    console.log(toState);
                    $timeout(function() {
                        $rootScope.title = (toState.data && toState.data.pageTitle)? toState.data.pageTitle: 'Default title';
                        $rootScope.metakeywords="this is keywords"
                    });
                };
                $rootScope.$on('$stateChangeSuccess', listener);
            }
        };
    }
]);
{%endcodeblock%}
这里赋值是通过获取当前state中设置的title，也就是这里toState对象的值，当我们打印这个toState时就会发现：
201608191020547.png
这里是获取的已经设置好的data中pageTitle的值，如果不想写在state里或者写死，可以传state中的唯一标示，配合后台接口，将查询的title渲染到页面；同样meta标签如keywords、description可以在此时一同绑定；
上面说到javascript框架在seo方面存在短板，应对ng的这个问题市面上也有很多方案,比如prerender，seo.js等，思想都是在页面加入表示，让爬虫在页面渲染好后才去扒数据，同时服务器上要配置些服务，服务将检测是否有对应这个URL的快照或者缓存的页面，如果存在就发给爬虫，如 果不存在，则生成快照，然后发送正确的页面给爬虫；处理起来还是要费些功夫的，所以也可以采用ng+常规的开发模式，一些重要的页面不要用这种页面渲染seo的方式，或者建立专门的seo信息页；所以在这方面感觉用ng框架做app（ionic）还是很合适的；


















{% blockquote %}
i love you
{% endblockquote %}