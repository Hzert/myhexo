---
title: vue element-ui—2
date: 2017-11-13 18:25:48
tags: [vue,前端]
categories: [前端, vue]
---
## element ui 里的日期选择器获取值的格式问题
1.官网的文档里有个 format="yyyy-MM-dd" 可以使用到 el-date-picker  日期选择组件内。

但是 加上了format以后，并没有什么用。
获取到的值还是一个obj 如下：
{%codeblock%}
Fri Sep 22 2017 00:00:00 GMT+0800 (中国标准时间)
{%endcodeblock%}

除了要使用format这个属性设置格式以外，在官方文档中有个change方法
{%codeblock%}
<el-date-picker type='date' v-model='setTime' @change='getTime' format='yyyy-MM-dd' placeholder='开始时间'>
</el-date-picker>
{%endcodeblock%} 

然后在methods中，添加一个方法即可
{%codeblock%}
getTime(val) {
  this.setTime = val  //这个setTime是在data中声明的，也就是v-model绑定的值
}
{%endcodeblock%}