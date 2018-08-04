---
title: vue-双向数据绑定原生js实现
date: 2018-05-04 17:23:51
tags: [vue]
categories: [前端, vue]
---
{%codeblock%}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<input type="text" id="aa"/>
<span id="bb">{{hello}}</span>
<script>
    var obj = {};
    Object.defineProperty(obj,'hello',{
        set:function(val){
            document.getElementById('bb').innerHTML = val;
            document.getElementById('aa').value = val;
        }
    });
    document.getElementById('aa').onkeyup = function(e){
        obj.hello = e.target.value;
    };
    obj.hello = "";


</script>
</body>
</html>
{%endcodeblock%}

`Object.defineProperty(obj, prop, descriptor)`

obj
要在其上定义属性的对象。
prop
要定义或修改的属性的名称。
descriptor
将被定义或修改的属性描述符。