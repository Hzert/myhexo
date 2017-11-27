---
title: 那些javascript面试题考核的知识点
date: 2017-11-27 18:54:09
tags: [javascript,前端]
categories: [编程,javascript]
---
## 1.预解析

预解析：在当前作用域下，js运行之前，会把带有var和function关键字的事先声明，但不会赋值

{%codeblock%}
alert(a);
a();
var a=3;
function a(){
  alert(10)
}
alert(a)
a=6;
a();
---------------- 分割线 --------------------------
alert(a);
a();
var a=3;
var a = function(){
  alert(10)
}
alert(a)
a=6;
a();
{%endcodeblock%}
看到这个代码，当时答错了。后来请教了朋友，然后自己再理解下，就理顺了！考点其实就两个，第一变量声明提前，第二函数声明优先于变量声明！下面我简单分析一下，第一部分运行结果：1.函数声明优先于变量声明，所以，刚开始，a就是function a(){alert(10)} ，就会看到这个函数。2.a()，执行函数，就是出现alert(10)3.执行了var a=3; 所以alert(a)就是显示34.由于a不是一个函数了，所以往下在执行到a()的时候， 报错。第二部分运行结果：1.underfind2.报错在之前说过，预解析是把带有var和function关键字的事先声明，但不会赋值。所以一开始是underfind，然后报错是因为执行到a()的时候，a并不是一个函数。//函数表达式，和变量声明同等
var a=function(){
    alert(10)
} 
//函数声明，优于变量声明    
function a(){
    alert(10)
} 
## 1-2.预解析和作用域
var a=0;
function aa(){
    alert(a)
    a=3
}
//结果是什么都没发生，因为要执行aa函数才会执行alert(0)

------------分割线1------------------
{%codeblock%}
var a=0;
function aa(){
    alert(a)
    var a=3
}
aa();
//underfind  在aa函数里面，有var a=3，那么在aa作用域里面，就是把a这个变量声明提前，但是不会赋值，所以是underfind

------------分割线2------------------

var a=0;
function aa(a){
    alert(a)
    var a=3
}
aa(5)
alert(a)
//5,0   在函数体内，参数a的优先级高于变量a

------------分割线3------------------

var a=0;
function aa(a){
    alert(a)
    a=3
}
aa(5)
alert(a)
//5,0   在函数体内，执行alert(a)和a=3,修改的的并不是全局变量a，而是参数a

------------分割线4------------------

var a=0;
function aa(a){
    alert(a)
    var a=3
    alert(a)
}
aa(5)
//5,3
//
//1.参数优先级高于变量声明，所以 变量a的声明其实被忽略了，此时相当于
//var a=0;
//function aa(a){
//  var a=5;
//    alert(a)
//    a=3
//    alert(a)
//}
//aa(5)

//2.形参和局部变量优先级一样，此时相当于
//var a=0;
//function aa(a){
//  var a;    先声明
//  a=5      由于形参和变量名称一样，覆盖了！
//    alert(a)
//    a=3
//    alert(a)
//}
//aa(5)

------------分割线5------------------

var a=0;
function aa(a){
    alert(a)
    a=3
    alert(a)
}
aa()
alert(a)
//underfind  3  0 
//首先，参数优先级高于全局变量，由于没传参数，所以是underfind
//a=3，实际上修改的时形参a的值，并不是全局变量a，往下alert(a)也是形参a
//最后的alert(a)，你懂的
{%endcodeblock%}
## 3.循环与递归
3-1.费波纳茨数组这个不多说了，很简单，但是很经典。就是当前项等于前两项的和

{%codeblock%}
var arr=[];
for(var i=0;i<10;i++ ){
    i<=1?arr.push(1):arr.push(arr[i-1]+arr[i-2]);
}
console.log(arr)3-2.数据排列比如 123454321 23456765432这个怎么做呢？当时我的做法的分两步写，先展示前面，再展示后面代码是//01234543210
//先展示前面的   01234
//n：开始的数字    m:结束的数字
function num1(n,m){
    for(var i=n;i<m;i++){
        //再展示后面的 543210
        console.log(i);
        if(i===m-1){
            num2(n,m)
        }
    }
}
function num2(n,m){
    for(var i=m;i>=n;i--){
        console.log(i)
    }
}
num1(2,5)  //2345432这样代码太多了，后来研究了这种function num(n,m){
    console.log(n);
    if(n<m){
        num(n+1,m);
        console.log(n);
    }
}
num(2,5)  //2345432解释如下1.首先执行num(2,5)，就是
console.log(2); ->  num(3,5);  ->  console.log(2);      
//执行num(3,5);  就是是相当于   console.log(3); -> num(4,5); -> console.log(3); 下面以此类推
console.log(2); -> console.log(3); -> num(4,5); -> console.log(3); ->  console.log(2);  

然后就是

console.log(2); -> console.log(3); -> console.log(4); -> num(5,5); -> console.log(4); -> console.log(3); ->  console.log(2);

最后就是

console.log(2); -> console.log(3); -> console.log(4); -> console.log(5); -> console.log(4); -> console.log(3); ->  console.log(2);
{%endcodeblock%}
## 4.其它

{%codeblock%}
function foo1()
{
 return {
     bar: "hello"
 };
}
 
function foo2()
{
 return
 {
     bar: "hello"
 };
}
var a=foo1();
var b=foo2();
console.log(a) //Object {bar: "hello"}
console.log(b) //underfind
//仔细看就知道了4-2网上看到的题目，我自己改造下 80%应聘者都不及格的JS面试题for (var i = 0; i < 5; i++) {
  console.log(i);
}
console.log(i);
//这个大家应该很快就知道了，012345



for (var i = 0; i < 5; i++) {
 setTimeout(function() {
  console.log(i);
 }, 1000);
}
console.log(i);
//这个大家就要小心一点了，答案是5    55555
//在setTimeout执行之前，for循环早就执行完了，i的值早已经是5了，所以一开始是执行，最后面的console.log(i);
//在for循环的时候一下子自定义5个setTimeout，大概一秒后，就是输出55555



for (var i = 0; i < 5; i++) {
 (function(j) { // j = i
  setTimeout(function() {
   console.log(j);
  }, 1000);
 })(i);
}
console.log(i); 
//这里的解析和上面基本一样，只是用闭包来记录每一次循环的i,
//所以答案是5     01234



var output = function (i) {
 setTimeout(function() {
  console.log(i);
 }, 1000);
};
 
for (var i = 0; i < 5; i++) {
 output(i); // 这里传过去的 i 值被复制了
}
console.log(i);

//这里的解析和上面基本一样，把i当参数传进output，记录每一次循环的i,
//所以答案是5     01234



for (let i = 0; i < 5; i++) {
 setTimeout(function() {
  console.log(i);
 }, 1000);
}
console.log(i);
//结果是  报错   01234 
//注意i是用let定义的，不是var

{%endcodeblock%}