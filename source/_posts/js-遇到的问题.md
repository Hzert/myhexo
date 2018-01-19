---
title: js-遇到的问题
date: 2018-01-09 15:16:36
tags: [javacript]
categories: [编程,javascript]
---

本篇纪录在工作中，或者平时学习的时候纪录的一些遇到的问题！


## 1、数组－字符串之间的转换

### 1.1 字符串转数组
{%codeblock%}
    $scope.string2Array = function (stringObj) { // 字符串转成数组
      var arr = []
      if(stringObj.indexOf('，') != -1) { // 中文逗号
        arr = stringObj.split('，')
      }else if (stringObj.indexOf(',') != -1) { // 英文逗号
        arr = stringObj.split(',')
      }else if (stringObj.indexOf('、') != -1) { // 顿号
        arr = stringObj.split('、')
      }else if (stringObj.indexOf(';') != -1) { // 分号
        arr = stringObj.split(';')
      }else if (stringObj.indexOf('；') != -1) { // 分号
        arr = stringObj.split('；')
      }else if (stringObj.indexOf('/') != -1) { // 斜杠
        arr = stringObj.split('/')
      }else if (stringObj.indexOf('／') != -1) { // 斜杠
        arr = stringObj.split('／')
      }else {
        arr = stringObj
      }
      var newArray = []; // new Array()
      if(arr instanceof Array){
        for ( var i = 0; i < arr.length; i++) {
          var arrOne = arr[i]
          newArray.push(arrOne)
        }
      }else{
        newArray.push(arr)
      }
      return newArray
    }
{%endcodeblock%}

 1. 从方法名就能知道这是一个字符串转数组的方法 用了字符串的方法  indexOf 判断用什么符号分割 indexOf=-1时表示检索的该字符没有在字符串中出现 indexOf返回指定字符在字符串中首次出现的位置
 2. split方法 **split(',')**  按照指定的**字符分割成字符串数组**  返回 **字符串数组**



## 2、对象的深拷贝
{%codeblock%}
var copyObj = JSON.parse(JSON.stringify(Obj||Array))
{%endcodeblock%}


浅拷贝
{%codeblock%}
一个简单的浅复制
var obj = { a:1, arr: [2,3] };
var shallowObj = shallowCopy(obj);

function shallowCopy(src) {
  var dst = {};
  for (var prop in src) {
    if (src.hasOwnProperty(prop)) {
      dst[prop] = src[prop];
    }
  }
  return dst;
}
{%endcodeblock%}

## 3、输入法  半角转全角  全角转半角   
主要是项目里有些输入框里面输入半角的特殊符号，加密解密的时候会出现错误

{%codeblock%}
/*
*
* @desc 半角转全角 
* @param 半角转全角 
* @return 输入法的半角转全角 
*/



    function ToDBC(txtstring) {                 // 字符串的 半角转全角 主要是进行特殊字符的判断，防止加密解密失败
      var tmp = ""; 
      for(var i=0;i<txtstring.length;i++){ 
        if(txtstring.charCodeAt(i)==32){ 
            tmp= tmp+ String.fromCharCode(12288); 
        } 
        if(txtstring.charCodeAt(i)<127){ 
            tmp=tmp+String.fromCharCode(txtstring.charCodeAt(i)+65248); 
        } 
      } 
      return tmp;
    }


/*
*
* @desc 全角转半角 
* @param 全角转半角  
* @return 全角转半角  
*/



    function ToCDB(str) { 
        var tmp = ""; 
        for(var i=0;i<str.length;i++){ 
            if (str.charCodeAt(i) == 12288){
                tmp += String.fromCharCode(str.charCodeAt(i)-12256);
                continue;
            }
            if(str.charCodeAt(i) > 65280 && str.charCodeAt(i) < 65375){ 
                tmp += String.fromCharCode(str.charCodeAt(i)-65248); 
            } 
            else{ 
                tmp += String.fromCharCode(str.charCodeAt(i)); 
            } 
        } 
        return tmp 
    } 

{%endcodeblock%}


## 4. 设置图片宽度，超过浏览器宽的100%显示

 id pageModules 是外面包裹着img的div  里面的img 撑开了div 导致出现滚动条，可以用以下方法进行处理
{%codeblock%}
 function setImgWidth() {
      // 设置图片宽度，超过浏览器宽的100%显示
      var app = document.getElementById('pageModules');
      var img = app.getElementsByTagName('img');
      for (var i = 0; i < img.length; i++) {
        (function (i) {
         var imgEl= document.createElement('img')
         imgEl.src=img[i].src
         imgEl.onload = function () {
            // alert(i)
            if (parseInt(getStyle(img[i], 'width')) > parseInt(getStyle(app, 'width'))) {
              img[i].style.width = '100%';
            }
          };
        })(i);
      }
    }
{%endcodeblock%}


## 5. js 数组里面很多对象，怎么判断对象里的某一个值跟其他对象的值相等

项目中有一个这样的需求：需要将一个数组里面的对象根据一个字段的值分成多个数组
比如有如下数据结构
{%codeblock%}
 "collectTotalMesg": [
        {
            "fieldName": "1",
            "id": 0,
            "selectType": "0",
            "selectDetai": "",
            "needCheck": "Y",
            "dealType": "add",
            "pageLoadIndex": "2",
            "moduleType": "3",
            "collectId": "",
            "collectIndex": "2"
        },
        {
            "fieldName": "2",
            "id": 0,
            "selectType": "1",
            "selectDetai": "1",
            "needCheck": "Y",
            "dealType": "add",
            "pageLoadIndex": "2",
            "moduleType": "3",
            "collectId": "",
            "collectIndex": "2"
        },
        {
            "fieldName": "3",
            "id": 0,
            "selectType": "2",
            "selectDetai": "2,3",
            "needCheck": "Y",
            "dealType": "add",
            "pageLoadIndex": "2",
            "moduleType": "3",
            "collectId": "",
            "collectIndex": "2"
        },
        {
            "fieldName": "1",
            "id": 0,
            "selectType": "0",
            "selectDetai": "",
            "needCheck": "Y",
            "isCopy": true,
            "dealType": "add",
            "pageLoadIndex": "3",
            "moduleType": "3",
            "collectId": "",
            "collectIndex": "3"
        },
        {
            "fieldName": "2",
            "id": 0,
            "selectType": "1",
            "selectDetai": "1",
            "needCheck": "Y",
            "dealType": "add",
            "pageLoadIndex": "3",
            "moduleType": "3",
            "collectId": "",
            "collectIndex": "3"
        },
        {
            "fieldName": "3",
            "id": 0,
            "selectType": "2",
            "selectDetai": "2,3",
            "needCheck": "Y",
            "dealType": "add",
            "pageLoadIndex": "3",
            "moduleType": "3",
            "collectId": "",
            "collectIndex": "3"
        }
    ]
{%endcodeblock%}

最终获得的数据,是以collectIndex的值 作为一个数组
![](/img/grouping2.png)
{%codeblock%}
function grouping(data) {
    var arg=[].slice.call(arguments,1),arr=data;
    for(var i=0,l=arg.length;i<l;i++){
        var newArr = [];
        if(arr[0].constructor === Array){
            arr.forEach(function(arrChild){
                newArr = newArr.concat(group(arrChild,arg[i]));
            })
        }else{
            newArr = group(arr,arg[i]);
        }
        arr = newArr;
    }
    function group(d,type){
        var num=0,typeCount=[],map={}
        d.forEach(function(obj){
            var value = map[String(obj[type])];
            if(value !== void 0){
                typeCount[value].push(obj);
            }else{
                map[obj[type]] = num;
                typeCount[num] = [].concat([obj]);
                num++;
            }
        });
        return typeCount;
    }
    return arr;
}

var data = [
  {name:"a",dir:"A"},
  {name:"a",dir:"A"},
  {name:"a",dir:"B"},
  {name:"a",dir:"B"},
  {name:"a",dir:"C"},
  {name:"b",dir:"A"},
  {name:"b",dir:"C"}
];
var a = grouping(data,"name","dir");
console.log(a)
{%endcodeblock%}
![](/img/grouping.png)


## 6. 将一个大数组内的数组转换成json 
{%codeblock%}
$scope.fakeData = $scope.a.map(function(v){
  return { collectList:v,moduleType: "3",pageLoadIndex:item.pageLoadIndex}
})

json 的key 是coollectList 

最后得到的一个这样结构的数组
[
  {collectList:[
    {
      "fieldName": "1",
      "id": 0,
      "selectType": "0",
      "selectDetai": "",
      "needCheck": "Y",
      "dealType": "add",
      "pageLoadIndex": "2",
      "moduleType": "3",
      "collectId": "",
      "collectIndex": "2"
    },
    {
      "fieldName": "1",
      "id": 0,
      "selectType": "0",
      "selectDetai": "",
      "needCheck": "Y",
      "dealType": "add",
      "pageLoadIndex": "2",
      "moduleType": "3",
      "collectId": "",
      "collectIndex": "2"
    }]
  },
  {collectList:[
    {
      "fieldName": "1",
      "id": 0,
      "selectType": "0",
      "selectDetai": "",
      "needCheck": "Y",
      "dealType": "add",
      "pageLoadIndex": "2",
      "moduleType": "3",
      "collectId": "",
      "collectIndex": "2"
    },
    {
      "fieldName": "1",
      "id": 0,
      "selectType": "0",
      "selectDetai": "",
      "needCheck": "Y",
      "dealType": "add",
      "pageLoadIndex": "2",
      "moduleType": "3",
      "collectId": "",
      "collectIndex": "2"
    }]
  }
]
{%endcodeblock%}