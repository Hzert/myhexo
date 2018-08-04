---
title: js面试题
date: 2018-05-04 16:51:13
tags: [javascript]
categories: [javascript]
---
1. Q1
{%codeblock%}
function doSomething(){
  for(var i=0;i<4;i++){
    var value = 100;
    str += ',' + (value + i);
  }
}
var value = 1, str = value;
doSomething();
str += value;
console.log(str)
{%endcodeblock%}


2. Q2
{%codeblock%}
var a = [];
a[0] = 0;
a[1] = 1;
a[4] = 4;
console.log(a.length);
console.log(a[3])
{%endcodeblock%}


3. Q3
{%codeblock%}
var a = [5,6];
var b = a;
b[0] = 'hello';
console.log(a[0])
{%endcodeblock%}

4. Q4
{%codeblock%}
console.log(undefined || 1);
console.log(null || NaN);
console.log(0 && 1);
console.log(0 && 1 || 0);
{%endcodeblock%}



5. Q5
{%codeblock%}
function Foo(){
  var i = 0;
  return function(){
    console.log(i++);
  }
}
var f1 = Foo(),f2 = Foo();
f1();
f2();
f2();
console.log(i)
{%endcodeblock%}


6. Q6
{%codeblock%}
var num = 1;
var fun = function(){
  console.log(num);
  var num = 2;
  console.log(num);
}
fun();
{%endcodeblock%}

7. Q7
{%codeblock%}
var a = [];
for(var i = 0; i<10;i++){
  a[i] = function(){
    console.log(i)
  }
};
a[6]();
var b = [];
for(let j=0;j<10;j++){
  b[j] = function(){
    console.log(j)
  }
};
b[6]();
{%endcodeblock%}

8. 8Q
{%codeblock%}
let[,,third] = ['foo','bar','baz'];
console.log(third)

let[head, ...tail] = [1,2,3,4];
console.log(tail)

let[x,y='b'] = ['a',undefined];
console.log(y);
let{foo:baz} = {foo:'aaa',bar:'bbb'}
{%endcodeblock%}


9. 9Q
{%codeblock%}
for(var i=0;i<5;i++){
  setTimeout(function(){
    console.log(new Date,i)
  },1000)
}
console.log(new Date,i)
{%endcodeblock%}

{%codeblock%}
var name = 'window';
var obj = {
  name: 'obj',
  getName: function(){
    console.log(this.name);
    return function(){
      console.log(this.name)
    }
  }
}
obj.getName()()
{%endcodeblock%}