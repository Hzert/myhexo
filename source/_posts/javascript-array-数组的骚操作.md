---
title: javascript-array-数组的骚操作
date: 2017-11-22 16:47:13
tags: [前端,数组,javascript]
categories: [编程]
---
## js 对象数组去重方法。
1. reduce()方法去重
实际项目中， 后台返回的数据一般是json形式的
{%codeblock%}
var arr = [
  {'name':'Apple','age':18,'sex':'男',id:1},
  {'name':'Blue','age':13,'sex':'女',id:2},
  {'name':'Colton','age':16,'sex':'男',id:3},
  {'name':'Double','age':19,'sex':'女',id:4},
  {'name':'Apple','age':18,'sex':'男',id:1},
]
{%endcodeblock%}
按照id去重， 保证id的唯一性，一般的项目都会是以id为准
{%codeblock%}
var hash = {}  //定义一个对象
arr = arr.reduce(function(item,next){
    hash[next.id]?"":hash[next.id] = true && item.push(next);
    return item
},[])
{%endcodeblock%}
![](/img/arrS1.png)

### reduce() 方法接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始缩减，最终为一个值。

语法：
### arr.reduce([callback, initialValue])

四个参数：
{%codeblock%}
[1,2,3,4,5].reduce(function(a,b,c,d){
  return d
},0)
// 返回一个数组 [1,2,3,4,5]
a => 上一次值
b => 当前值
c => 当前值的索引
d => array 数组


求和。
[1,2,3,4,5].reduce(function(a,b){
  return a+b
},0)
// 15
{%endcodeblock%}

## 两个数组比较  骚操作去重
{%codeblock%}
var a=[{id:1},{id:2},{id:3}]
var b=[{id:4},{id:2},{id:3}]

function c(o){
  return  b.some(function(v){
      return v.id===o.id
  })
}
var d=a.filter(function(o){
  console.log(c(o))
  return !c(o)
})
console.log(d)
{%endcodeblock%}

### filter() 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素
{%codeblock%}
var a=[{id:1},{id:2},{id:3}]
var b = a.filter(function(item){
  return item.id == 1
})
//[{id:1}]
var b = a.filter(function(item){
  return item.id!==1
})
{%endcodeblock%}

### ome 为数组中的每一个元素执行一次 callback 函数，直到找到一个使得 callback 返回一个“真值”（即可转换为布尔值 true 的值）。如果找到了这样一个值，some 将会立即返回 true。否则，some 返回 false。callback 只会在那些”有值“的索引上被调用，不会在那些被删除或从来未被赋值的索引上调用。

callback 被调用时传入三个参数：元素的值，元素的索引，被遍历的数组。

如果为 some 提供了一个 thisArg 参数，将会把它传给被调用的 callback，作为 this 值。否则，在非严格模式下将会是全局对象，严格模式下是 undefined。

some 被调用时不会改变数组。

some 遍历的元素的范围在第一次调用 callback. 时就已经确定了。在调用 some 后被添加到数组中的值不会被 callback 访问到。如果数组中存在且还未被访问到的元素被 callback 改变了，则其传递给 callback 的值是 some 访问到它那一刻的值。
{%codeblock%}
var a = [1,23,12,12,34]
a.some(function(item){
  return item>10
})
// true
{%endcodeblock%}
