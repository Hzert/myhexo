---
title: javascript-数组操作
date: 2017-10-26 13:15:38
tags: [javascript,前端]
categories: [javascript]
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

3.forEach 遍历数组
{%codeblock%}
var first = [0,1,3,4,5,63];
first.forEach(function(item,index,array){
  console.log(item,index);
});
// 0  0
// 1  1
// 2  2
{%endcodeblock%}

## 取数组最大值，最小值
{%codeblock%}
Math.max.apply(null,[1,2,3,43,4])
Math.min.apply(null,[1,2,3,42,4])
{%endcodeblock%}

### 添加元素到数组的末尾  push()到数组末尾 添加
{%codeblock%}
var fruits = ['apple','Banana']
var newLength = fruits.push('Orange');
console.log(newLength)
// ['apple','Banana','Orange']
{%endcodeblock%}

### 删除数组末尾的元素 pop() 删除
{%codeblock%}
let last = fruits.pop();
//remove Orange(from the end)
//['apple,Banana'];
{%endcodeblock%}

### 删除数组最前面（头部）的元素  shift()
{%codeblock%}
  let first = fruits.shift();
  // remove apple from the front
  //['Banana']
{%endcodeblock%}

### 添加到数组的前面（头部） unshift()
{%codeblock%}
let newLength = fruits.unshift('Strawberry');
// add to the front
// ['Strawberry','Banana'];
{%endcodeblock%}

### 找到某个元素在数组中的索引  indexOf()
{%codeblock%}
fruits.push('Mango');
// ['Strawberry','Banana','Mango'];

let index = fruits.indexOf('Banana');
//1
{%endcodeblock%}

### 通过索引删除某个元素  splice(pos,index)
{%codeblock%}
let removedItem = fruits.splice(pos,1)
//['Strawberry','Mango']
{%endcodeblock%}

### 从一个索引位置删除多个元素
{%codeblock%}
let vegetables = ['Cabbage','Turnip','Radish','Carrot'];
console.log(vegetables);
//['Cabbage','Turnip','Radish','Carrot']

let pos = 1, n = 2;

let removedItems = vegetables.splice(pos,n);
console.log(vegetables);
//['Cabbage','Carrot']

console.log(removedIetms);
//['Turnip','Radish']
{%endcodeblock%}

### 复制一个数组   slice()
{%codeblock%}
var shallowCopy = fruits.slice();
//['Strawberry','Mango']
{%endcodeblock%}

## es6里的一些数组方法

### 1.使用Set处理数组去重和元素剔除问题
Set是es6新增的一种数据结构，它和数组非常相似，但是成员的值都是唯一的，没有重复的值。它提供了4个语义化的API：
{%codeblock%}
1.add(value):添加某个值，返回Set结构本身
2.delete(value)：删除某个值，返回一个布尔值，表示删除是否成功
3.has(value):返回一个布尔值，表示该值是否为Set的成员
4.clear():清除所有成员，没有返回值。
{%endcodeblock%}

那么我们可以用Set来干嘛呢？

第一个用法，数组去重。对于一个一维数组，我们可以先把它转化成Set，再配合...解构运算符重新转化为数组，达到去重的目的。请看例子：
{%codeblock%}
const arr = [1,1,2,2,3,4,5,5]

const newArr = [...new Set(arr)]
console.log(newArr)
// [1,2,3,4,5]
{%endcodeblock%}

值得注意的是，这个方法不能对元素为对象的数组奏效：
{%codeblock%}
const arr = [{ name: 'Alice', age: 12 },{ name: 'Alice', age: 12 },{ name: 'Bob', age: 13}]
const newArr = [...new Set(arr)]
console.log(newArr)
// [{ name: 'Alice', age: 12 },{ name: 'Alice', age: 12 },{ name: 'Bob', age: 13}]
{%endcodeblock%}

这是因为Set判断元素是否重复的办法类似于===运算符，两个对象总是不相等的。

除了去重，Set提供的delete()方法也是非常实用。在以往的做法中，如果要删除数组中指定的元素，我们需要先获取该元素所在下标，然后通过splice()方法去删除对应下标的元素，在理解上容易引起混乱：
{%codeblock%}
// 我想删除数组当中值为2的元素
const arr = [1, 2, 3]
const index = arr.indexOf(2)
if (index !== -1) {
    arr.splice(index, 1)
}

console.log(arr)

// [1, 3]
{%endcodeblock%}

使用Set就清晰多了：
{%codeblock%}
const arr = [1, 2, 3]
const set = new Set(arr)
set.delete(2)
arr = [...set]

console.log(arr)

// [1, 3]
{%endcodeblock%}

### 2、 使用map()方法和对象解构语法提取字段
请求后台接口返回的数据中，很可能会遇到下面这种数据格式：
{%codeblock%}
studentInfo = [
  { name: 'Alice', age: 18, no: 2 },
  { name: 'Bob', age: 16, no: 5 },
  { name: 'Candy', age: 17, no: 3 },
  { name: 'Den', age: 18, no: 4 },
  { name: 'Eve', age: 16, no: 1 },
]
{%endcodeblock%}

当我们要获取姓名列表、年龄列表和编号列表的时候，我们可以通过map()再配合对象的解构语法方便快捷地进行处理：
{%codeblock%}
const nameList = studentInfo.map(({ name }) => name)
const ageList = studentInfo.map(({ age }) => age)
const noList = studentInfo.map(({ no }) => no)

// nameList: [ 'Alice', 'Bob', 'Candy', 'Den', 'Eve' ]
// ageList: [ 18, 16, 17, 18, 16 ]
// noList: [ 2, 5, 3, 4, 1 ]
{%endcodeblock%}

### 3、使用filter()方法和对象解构语法过滤数组
接上上面的例子，如果我想获取一个“年龄小于等于17岁”的新列表，应该怎么做呢？类似map()方法，我们可以用filter()方法进行过滤：
{%codeblock%}
const newStudentInfo = studentInfo.filter(({ age }) => {
  return age <= 17
})

/*
newStudentInfo: [
  { name: 'Bob', age: 16, no: 5 },
  { name: 'Candy', age: 17, no: 3 },
  { name: 'Eve', age: 16, no: 1 }
]
*/
{%endcodeblock%}

### 4、借助includes()方法求两个数组的差集

假设我们有以下两个数组：
{%codeblock%}
var a = [1, 2, {s:3}, {s:4}, {s:5}]
var b = [{s:2}, {s:3}, {s:4}, 'a']
{%endcodeblock%}

我们应该如何找到它们的差集呢？传统的方法可能需要把它们以Object形式hash化，但其实我们可以通过.includes()方法更加优雅方便地找出差集，代码如下：
{%codeblock%}
var a = [1, 2, {s:3}, {s:4}, {s:5}].map(item => JSON.stringify(item))
var b = [{s:2}, {s:3}, {s:4}, 'a'].map(item => JSON.stringify(item))

var diff = a.concat(b)
            .filter(v => !a.includes(v) || !b.includes(v))
            .map(item => JSON.parse(item))
            
// diff: [1, 2, {s:5}, {s:2}, "a"]
{%endcodeblock%}

至于为什么要JSON.stringify()，是因为要对比两个“对象元素”是否相等，是无法直接以“对象”形式比较的（永远返回不相等）。