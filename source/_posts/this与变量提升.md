---
title: this与变量提升
tags: [javascript,前端]
categories: [javascript]
---
## 1、变量提升 var 

{%codeblock%}
a = 'ghostwu';
var a;
console.log(a);   // gostwu
{%endcodeblock%}

`consle.log(a);`
`var a = 'ghostwu'`    // undefined
等价于 => 
    `var a ;`       // 变量提升
    `console.log(a);`
    `a = 'ghostwu'`


javascript 程序并不全是一行一行往下执行的
1. 词法解释（翻译）    // `在整个文件中查找带 var 声明的变量，把声明提前到当前作用域的最前面`
2. 运行阶段（把代码从上往下 按程序执行）


{%codeblock%}
function show(){
  console.log('1')
}
show()
{%endcodeblock%}
`函数声明回提升到当前作用域的最前面`

`表达式不会提升`
{%codeblock%}
show();
var show = function(){
  console.log('2')
}                           // 报错
=>
var show;
show();
show= = function(){
  console.log('2')
}                           // 报错
{%endcodeblock%}

{%codeblock%}
function show(){
  console.log(a);
  var a = '11122233'
}
show()                          // undefined
=>
function show(){
  var a;
  console.log(a);
  a = '11122233'
}                             // a不存在。console出来是undefined
{%endcodeblock%}

`当出现函数声明与变量声明 同名的情况 函数声明会被优先提升，变量声明会被忽略，表达式不会提升`
`如果出现多个同名的函数声明，后面的会把前面的覆盖`
{%codeblock%}
show();
var show;
function show(){
  console.log('2')
}
show = function(){
	console.log('21')
}
=>
function show(){
  console.log('2')
}
show();
show = function(){
	console.log('21')
}                             // 执行了console.log('2')
{%endcodeblock%}

{%codeblock%}
var a = true;
show();
if (a) {
  function show(){
    console.log('123')
  }
}else {
  function show(){
    console.log('456')
  }
}
//   会报错。 show不是一个函数～
{%endcodeblock%}
`因为函数声明提升只在当前作用域下，show()在if的作用域中，不是全局的 所以show()调用无效`

## 2、this 指向
`单独的this，指向window`
{%codeblock%}

alert(this)   //  this => window
this: 上下文，会根据执行环境的变化，而发生改变
{%endcodeblock%}

`全局函数中的this`
{%codeblock%}
function show() {
  alert(this)       //this => window
}
{%endcodeblock%}

{%codeblock%}
function show() {
  alert(this)       //this => object
}
var a = new show()
{%endcodeblock%}

`call apply 的this`
{%codeblock%}
  function show(a,b){
    alert(this)
  }
  show.call('abc')     // this => abc
  show.call(null)
  show.call(undefined)   // this => window
  show.call('abc',10 ,20)     // this => abc    call 后面跟一个一个的参数 
{%endcodeblock%}

{%codeblock%}
function show(a,b){
    alert(this)
  }
  show.apply('abc', [10, 20])     // this => abc  apply 参数是数组
 
{%endcodeblock%}

`定时器中的this, 指向的是window`
`元素绑定事件，事件触发后执行的函数中的this,指向的是当前的元素`
{%codeblock%}
setTimeout(function(){
  alert(this)           // this => window
},0)
{%endcodeblock%}

`函数调用时，如果绑定了 bind 那么函数中的this指向bind 中绑定的东西`
{%codeblock%}
window.onload = function(){
  var oBtn = document.querySelector('input')
  oBtn.addEventListener('click', function(){
    alert(this.a);
  }.bind(window));
}
{%endcodeblock%}

`对象中的方法，该方法被哪个对象调用，那么方法中的this就指向该对象`

{%codeblock%}
var obj = {
  show: function(){
    alert(this);   // this => obj
  }
}
obj.show();
{%endcodeblock%}

{%codeblock%}
var obj = {
  show: function(){
    alert(this);   // this => obj
  }
}
var fn = obj.show;    //  重新赋值给全局变量
fn();               // this => window
{%endcodeblock%}

`腾讯笔试题`
{%codeblock%}
var x = 20;
var a = {
  x: 15,
  fn: function(){
    var x = 30;
    return function () {
      return this.x;
    }
  }
};
console.log(a.fn());    // function 对象调用方法，return 一个函数
console.log( (a.fn())() );  // 20   函数表达式执行，自执行表达式的this指向window
console.log(a.fn()());  // 20       执行函数，当成闭包调用,this指向window
console.log(a.fn()() == (a.fn()()));  // true
console.log(a.fn().call(this));     // 20    把window传给了this.x
console.log(a.fn().call(a));        // 15     指向a对象。this.x = 15
{%endcodeblock%}