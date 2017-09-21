---
title: 你不知道的css
date: 2017-09-21 10:39:01
tags: [css]
categories: [编程]
---



### 用font-size来清除间距

inline-block的元素之间会受到空白区域的影响，也就是元素之间差不多会有一个字符的间隙。如果在同一行内有4个25%相同宽度的元素，会导致最后一个元素掉下来。 这个之前在张鑫旭大神那里看了inline-block布局，就提到怎么解决这个问题。可以利用元素浮动float，或者压缩html，清除元素间的空格来解决。但是最简单有效的方法还是设置父元素的font-size属性为0。


{%codeblock%}
*{
    box-sizing:border-box;
}
.items{
    font-size:0;
    > .item{
        display:inline-block;
        width:25%;
        height:50px;
        border:1px solid #ccc;
        text-align:center;
        line-height:50;
        background-color:#eee;
        font-size:16px;
    }
}
{%endcodeblock%}

{%codeblock%}
<div class="items">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
</div>
{%endcodeblock%}


### 用overflow来清除浮动

overflow除了定义溢出元素内容区的内容会如何处理外，还可以做一些有用的事，如：
    1.创建块格式化上下文
    2.清除浮动
假如你的案例中没有对溢出的操作（如下拉菜单），推荐使用overflow:hidden来清除浮动。
{%codeblock%}
.clearfix{
    overflow:hidden;
}
{%endcodeblock%}

{%codeblock%}
<div class="clearfix">
    <div class="left">left</div>
    <div class="right">right</div>
</div>
{%endcodeblock%}


### 用border来绘制三角形

{%codeblock%}
.border-arrow{
    width:256px;
    height:256px;
    border:48px solid;
    border-top-color:red;
    border-right-color:blue;
    border-bottom-color:green;
    border-left-color:orange;
}
{%endcodeblock%}
如果将盒子的宽度和高度设为0，盒子将展现出由四个三角形组成的矩形

{%codeblock%}
.border-arrow{
    width:0;
    height:0;
    border-width:96px;
}
{%endcodeblock%}
只需要将其他三个边的颜色设为透明（transparent或者rgba(0,0,0,0)）,就会只保留一个三角形

{%codeblock%}
.border-arrow{
    width:256px;//保持宽高，盒子就会呈现为一个梯形
    height:256px;
    border:64px solid;
    border-color:red transparent transparent transparent;
}
{%endcodeblock%}


### 用pointer-event来禁用事件
    pointer-event属性更像是一个javascript事件，利用改属性，可以做如下的事情：
        1.阻止任何点击动作的执行
        2.是链接显示为默认光标(cursor:default)
        3.阻止触发hover和active状态
        4.阻止javascript点击事件的触发
{%codeblock%}
.disabled{
    pointer-events:none;  //使用该类,任何点击事件将无效
}
{%endcodeblock%}

### 用max-width来防止图片撑破容器
针对内容性的文案，图片大小都是未知的，为了防止图片过大而撑破容器，可以通过设置图片的max-width:100%来处理；
{%codeblock%}
img{
    display:inline-block;
    max-width:100%;
}
{%endcodeblock%}


### 未知高度容器的多种垂直居中方法
    在一直父子高度的情况下，实现垂直居中是很容易的事。margin,padding,absolute+负margin,甚至于line-height都是可行的方案。
    在父容器高度固定，子容器高度自适应的情况下。来实现其垂直居中于父级盒子的几种方案

### 伪元素占位方案 （推荐）
利用伪元素和display:inline-block的方案来实现垂直居中

{%codeblock%}
    .vh-modal-1{
        text-align:center;//水平居中
        font-size:0;//消除空隙
    }
    .vh-modal-1::before{  //主要就是给父元素添加伪元素
        content:"";
        heigth:100%;
        display:inline-block;
        vertical-align:middle;
        font-size:14px;
    }
    .vh-modal-content{
        display:inline-block;
        vertical-align:middle;
        font-size:14px;
    }
   
{%endcodeblock%}

{%codeblock%}
<div class="vh-modal vh-modal-1">
  <div class="vh-modal-content">
    <h3 class="vh-modal-title">模态框</h3>
    <div class="vh-modal-body">...</div>
    <div class="vh-modal-foot">
      <button class="btn btn-primary">确定</button>
    </div>
  </div>
</div>
{%endcodeblock%}

### absolute + transform方案
使用absolute绝对定位子元素，并且设置其top:50%;left:50%,然后利用css3的transform:translate(-50%,-50%);设置负值偏移回来也是一种有效的垂直居中的方案，但是要注意其兼容性以及不要将子容器置于父容器半个像素的位置上，否则子容器会出现模糊

{%codeblock%}
.vh-modal-2 .vh-modal-content{
    //尽可能的不要让该元素的宽度或者高度出现奇数，否则可能会导致模糊
    display:inline-block;//为了自适应宽度，可以固定宽度
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
}
{%endcodeblock%}


### table-cell方案
使用div来模拟table的行为也可以实现垂直居中，缺点是要在子容器外层再包裹一个父元素 vh-modal-cell用来模拟table-cell

{%codeblock%}
.vh-modal-3{
    display:table;
    width:100%;
}
.vh-modal-3 .vh-modal-cell{
    display:table-cell;
    vertical-align:middle;
    text-align:center;
}
.vh-modal-content{
    display:inline-block;
}
{%endcodeblock%}

### 基于flex的方案  （强烈推荐）
毫无疑问，flex盒模型是最佳的实践方案。目前几乎所有现代浏览器都支持flex布局，尤其是移动端（部分机型UC浏览器效果太差，差评😞）。
基于flex盒模型的水平垂直居中有如下两种方案：

{%codeblock%}
<div class="vh-modal vh-modal-4(5)">
  <div class="vh-modal-content">
    ...
  </div>
</div>
{%endcodeblock%}

## align-items&justify-content方案
{%codeblock%}
.vh-modal-4 {
  display: flex;
  align-items: center;
  justify-content: center;
  >.vh-modal-content {}
}
{%endcodeblock%}

### flex + margin 方案
这个方案是最神奇的，仅仅给子元素设置了margin:auto;属性，一切就这么发生了😱
{%codeblock%}
.vh-modal-5 {
  display: flex;
  margin: 0;
  >.vh-modal-content {
    margin: auto;
  }
}
{%endcodeblock%}

### 用USER-SELECT来禁用文本选中

在远古时代，如果你不想让别人选中你页面的内容，JavaScript是不可或缺的。而在文明社会中，只需要一句user-select:none的CSS样式就可以解决。IE6-9不支持该属性，可以通过给body添加onselectstart="return false;"的内联JavaScript语句搞定。
{%codeblock%}
body{
  user-select: none; //页面中的文本不能被选中
}
{%endcodeblock%}



转自https://smohan.net/blog/tr6bta