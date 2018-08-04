---
title: javascript面向对象
tags: [javascript,前端]
categories: [javascript]
---

1. new Object创建对象
{%codeblock%}
var obj = new Object();
obj.userName = '111222';
obj.showUserName = function(){
  return obj.userName;
}
{%endcodeblock%}
2. 简单工厂模式创建对象
{%codeblock%}
function create(uName){
  var obj = new Object();
  obj.userName = uName;
  obj.showUserName = function(){
    return obj.userName;
  }
  return obj;
}

var obj = create('sadas');
alert(obj.showUserName())
{%endcodeblock%}

3. 构造函数
`函数前面用new调用 就把它叫做构造函数`
{%codeblock%}
function create(uName){
  // 不需要手动new object
  this.userName = uName;
  this.showUserName = function(){
    return this.userName;
  }
  // 会自动把this return 出来
}

var obj = new create('sadas');
alert(obj.showUserName())
{%endcodeblock%}

## prototype原型对象
{%codeblock%}
function create(uName){
  this.userName = uName;
  <!-- this.showUserName = function(){
    return this.userName;
  } -->
  // 会自动把this return 出来
}
create.prototype.showUserName = function(){
  return this.userName;
}


var obj = new create('sadas');
var obj2 = new create('szxc');
alert(obj.showUserName())
alert(obj.showUserName === obj2.showUserName)         // true
{%endcodeblock%}
`原型对象prototype`
`1.每个函数上面都有一个原型属性【prototype】,这个【prototype】会指向构造函数的原型对象`
`2.每个函数的原型对象【默认都有constructor属性指向构造函数本身`
`3.每个实例都有一个隐式原型（_proto_）指向构造函数的原型对象`