---
title: jsonP跨域做法-面试时的漏洞
date: 2018-04-25 21:44:57
tags: [jsonp]
categories: [javascript]
---

`ajax经过jQuery封装后的跨域做法`
`重点是dataType属性，设置为jsonp，就能实现jsonp跨域`

{%codeblock%}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery实现JSONP</title>
</head>
<body>
    <div id="mydiv">
        <button id="btn">点击</button>
    </div>
</body>
<script type="text/javascript" src="https://code.jquery.com/jquery-3.1.0.min.js"></script>
<script type="text/javascript">
    $(function(){
        $("#btn").click(function(){

            $.ajax({
                async : true,
                url : "https://api.douban.com/v2/book/search",
                type : "GET",
                dataType : "jsonp", // 返回的数据类型，设置为JSONP方式
                jsonp : 'callback', //指定一个查询参数名称来覆盖默认的 jsonp 回调参数名 callback
                jsonpCallback: 'handleResponse', //设置回调函数名
                data : {
                    q : "javascript", 
                    count : 1
                }, 
                success: function(response, status, xhr){
                    console.log('状态为：' + status + ',状态是：' + xhr.statusText);
                    console.log(response);
                }
            });
        });
    });
</script>
</html>
{%endcodeblock%}


`JSONP 是 JSON with padding（填充式 JSON 或参数式 JSON）的简写。`

`JSONP实现跨域请求的原理简单的说，就是动态创建<script>标签，然后利用<script>的src 不受同源策略约束来跨域获取数据。`

`JSONP 由两部分组成：回调函数和数据。回调函数是当响应到来时应该在页面中调用的函数。回调函数的名字一般是在请求中指定的。而数据就是传入回调函数中的 JSON 数据。`

`动态创建<script>标签，设置其src，回调函数在src中设置：`
{%codeblock%}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JSONP实现跨域2</title>
</head>
<body>
    <div id="mydiv">
        <button id="btn">点击</button>
    </div>
</body>
<script type="text/javascript">
    function handleResponse(response){
      console.log(response);
    }
</script>
<script type="text/javascript">
  window.onload = function() {

  var oBtn = document.getElementById('btn');

  oBtn.onclick = function() {     

      var script = document.createElement("script");
      script.src = "https://api.douban.com/v2/book/search?q=javascript&count=1&callback=handleResponse";
      document.body.insertBefore(script, document.body.firstChild);   
  };
};
</script>
</html>
{%endcodeblock%}