---
title: javascript-数组操作
date: 2017-10-26 13:15:38
tags: [javascript,前端]
categories:
---
在实际的一些项目中，有很多都是用到数组的一些操作，所以今天先把数组的一些方法和函数学习学习。

### Array数组对象用来在单独的变量名中存储一系列的值

可以存储多个不同类型的数据

#### 定义数组
{%codeblock%}
var arr = new Array()  //new 关键字定义数组
{%endcodeblock%}

### 赋值
{%codeblock%}
第一种
var arr = new Array();
arr[0]="1"
arr[1]='2'
arr[2]='3'
console.log(arr)  =>   ['1','2','3']

第二种
var array = new Array('1','2',3)

console.log(array)  =>  ['1','2',3]

第三种
var arr1 = new Array(10)

console.log(arr1)  => []   length为10

通常用的
var arr = [];   //空数组
var arr1 = [1,2,3,4,5];   // 数据一般就写在中括号里,多个数据用逗号分割
{%endcodeblock%}

### 数组的访问

数组元素的访问：
{%codeblock%}
var arr = [1,2,3,4,5]

console.log(arr[3])  => 4   //数组名+[index] 中括号里面放入数组的index下标 （index从0开始）
{%endcodeblock%}
![](/img/array1.jpg)

### 数组的遍历

1.快速遍历  for in
{%codeblock%}
var arr = [1,2,3,4,5];
var sum = 0;
for(var j in arr){
  console.log(j); //0,1,2,3,4
  console.log(arr[j]);  //1,2,3,4,5
}
{%endcodeblock%}

2.for 循环遍历
{%codeblock%}
var arr = [1,2,3,4,5]
for(var i=0;i<arr.length;i++){
  console.log(arr[i]);   //1,2,3,4,5
  console.log(i);        //0,1,2,3,4
}
{%endcodeblock%}