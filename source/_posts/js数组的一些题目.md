---
title: js数组的一些题目
date: 2018-03-02 15:57:43
tags: [javascript, 前端]
categories: [javascript]
---
记录一些数组的题目，面试也许会遇到

## 一、将下列数组求和（办法越多越好）
{%codeblock%}
var arr = [1,2,3,4,5,6,7,8,9];
{%endcodeblock%}
{%codeblock%}

  // for循环遍历数组求和
  function addArray1(array){
    var sum = 0;
    var len = array.length;
    for(var i=0;i<len;i++){
      sum += parseInt(array[i])
    }
    return sum;
  }
  
  // while循环遍历数组求和
  function addArray2(array){
    var sum = 0;
    var len = array.length;
    while(len--){
      sum += parseInt(array[len]);
    }
    return sum
  }

  // 用数组归并方法reduce进行数组求和
  function addArray3(array){
    var num = array.reduce(function(pre,cur,index,arr){
      return pre+cur;
    });
    return num;
  }
  
  // forEach()迭代方法，在回调函数中做一个累加计算
  function addArray4(array){
    var sum = 0;
    array.forEach(function(item,index,arr){
      sum += item;
    })
    return sum;
  }

  // some()迭代方法，在回调函数中做一个累加计算
  function addArray5(array){
    var sum = 0;
    array.some(function(item,index,array){
      sum += item;
    })
    return sum;
  }

  // map()迭代方法，在回调函数中做一个累加计算
  function addArray6(array){
    var sum = 0;
    array.map(function(item,index,array){
      sum += item;
    })
    return sum;
  }

  // filter()迭代方法，在回调函数中做一个累加计算
  function addArray7(array){
    var sum = 0;
    array.filter(function(item,index,array){
      sum += item;
    })
    return sum;
  }

  // every()迭代方法，在回调函数中做一个累加计算
  function addArray8(array){
    var sum = 0;
    array.every(function(item,index,array){
      sum += item;
    })
    return sum;
  }
{%endcodeblock%}

## 二、数组去重的方法
{%codeblock%}
var arr = [1,2,1,1,3,2,5]
{%endcodeblock%}
{%codeblock%}

//双重for循环 通过判断第一位是否与第二位是否相等，删除后面重复元素
  function dedup(array){
    var len = array.length;
    for(var i=0;i<len;i++){
      for(var j=i+1;j<len;j++){
        if(array[i] == array[j]){
          array.splice(j,1);
          j--;
        }
      }
    }
    return array;
  }

  //借助indexOf()方法判断此元素在改数组中首次出现的位置下标与循环的下标是否相等
  function dedup1(array){
    var len = array.length;
    for(var i=0;i<len;i++){
      if(array.indexOf(array[i]) !=1 ){
        array.splice(i,1);
        i--;
      }
    }
    return array;
  }

  // 利用数组中的filter方法
  function dedup2(array){
    var r = array.filter(function(element,index,self){
      return self.indexOf(element) === index;
    })
    return r;
  }

  //利用空对象来记录新数组中已经存储过的元素
  var o = {};
  var newArr = []
  for(var i=0;i<arr.length;i++){
    var k = arr[i];
    if(!o[k]){
      o[k] = true;
      newArr.push(k);
    }
  }
  console.log(newArr);

  //借助新数组 判断新数组中是否在该元素如果不存在将此元素添加到新数组中
  Array.prototype.reArr = function(){
    var newArr = [];
    for(var i=0;i<this.length;i++){
      if(newArr.indexOf(this[i]) == -1){
        newArr.push(this[i])
      }
    }
    return newArr;
  }

  //es6 set处理数组去重
  const arr = [1,1,2,2,3,4,5,5]
  const newArr = [...new Set(arr)]
  console.log(newArr)
  // [1,2,3,4,5]


  // 重点！！！！数组对象去重
  var arr = [
    {'name':'apple','age':18,'sex':'男'},
    {'name':'bule','age':17,'sex':'女'},
    {'name':'double','age':16,'sex':'女'},
    {'name':'apple','age':18,'sex':'男'}
  ]
  // 按照随便一个属性去重，比如是age
  var hash = {};
  arr = arr.reduce(function(item,next){
    hash[next.age]?'':hash[next.age] = true && item.push(next);
    return item;
  },[])

  // 两个数组比较，然后去重 以id为比较，在实际项目中会用到
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

## 从两个数组中取相同的元素
{%codeblock%}
var arr4 = [1,2,3,4,5,6,7,8]
var arr5 = [2,3,4,5]

// some() + filter() 方法处理

  function a(item){
    return arr5.some(function(v){
      return v === item
    })
  }
  var abc = arr4.filter(function(item){
    return a(item)
  })
  console.log(abc) // [2,3,4,5]
  // 用法跟上面的去重一样，用some方法进行判断符合的值，然后用filter方法进行筛选得到一个新数组


// 传入两个数组，循环判断第一个数组的元素在第二个数组中有没有，有的话放入新的数组
  function  FilterData(first,second){
    var result = new Array(); // 创建新的数组
    var newArray = second.toString();
    for(var i=0;i<first.length;i++){
      if(newArray.indexOf(first[i].toString())>-1){
        esult.push(first[i]);
      }      
    }
    return result;
  }
{%endcodeblock%}

## 将下面数组中的7和8对调位置
{%codeblock%}
var arr6 = [1,2,3,4,5,6,7,8,9]

arr6[6] = 8;
arr[7] = 7;

{%endcodeblock%}