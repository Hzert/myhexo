---
title: flex布局学习
date: 2017-10-13 13:24:27
tags: [手机端, css]
categories: [前端]
---
布局的传统解决方案，基于盒状模型，依赖 display 属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。

Flex 布局将成为未来布局的首选方案

### 任何容器都可以指定flex布局**
{%codeblock%}
.box{
    display: flex;
}
{%endcodeblock%}

### 行内元素也可以使用flex布局
{%codeblock%}
span{
    display: inline-flex;
}
{%endcodeblock%}

### webkit内核的浏览器，要加上-webkit前缀
{%codeblock%}
.box{
    display:-webkit-flex;/*safari*/
    display:flex;
}
{%endcodeblock%}

## 注意，设置未flex之后，float,clear和vertical-align都将失效

看代码：
{%codeblock%}
.box{
    display: flex;
    width:500px;
    height:500px;
    border:1px solid #1bb9c9;
}
.item{
    width:100px;
    height:100px;
    background: red;
}

css
******************************
html

<div class="box">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</div>
{%endcodeblock%}
![](/img/flex2.jpg)

当给box设置为flex布局以后，原本是box下的item应该是各占一行的。但是现在排成一行

## 有flex布局的容器有以下6种属性 ，这个容器是指上面代码的box
{%codeblock%}
flex-direction   //主轴方向（项目排列方向）
flex-wrap       //定义换行
flex-flow       //上面两个的简写
justify-content //定义在主轴上的对齐方式
align-items     //定义交叉轴如何对齐
align-content   //定义多根轴线的对齐方式
{%endcodeblock%}

### flex-direction决定项目的排列方向，项目指容器内部的子元素，比如上面代码的item
{%codeblock%}
.box{
    flex-direction: row | row-reverse | clumn | clumn-reverse;
}
{%endcodeblock%}

它可能有4个值
{%codeblock%}

row（默认值）：主轴为水平方向，起点在左端。

row-reverse：主轴为水平方向，起点在右端。

column：主轴为垂直方向，起点在上沿。

column-reverse：主轴为垂直方向，起点在下沿。

{%endcodeblock%}

### flex-wrap  定义换行
{%codeblock%}
.box{
    flex-warp: nowarp | warp | warp-reverse;
}
{%endcodeblock%}

它有3个值
{%codeblock%}

nowrap（默认）：不换行。

wrap：换行，第一行在上方。

wrap-reverse：换行，第一行在下方。

{%endcodeblock%}

### flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
{%codeblock%}
.box{
    flex-flow:(flex-direction) || (flex-wrap);
}
{%endcodeblock%}

### justify-content 定义在主轴上的对齐方式
{%codeblock%}
.box{
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
{%endcodeblock%}

它有5个值
{%codeblock%}

flex-start（默认值）：左对齐

flex-end：右对齐

center： 居中

space-between：两端对齐，项目之间的间隔都相等。

space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

{%endcodeblock%}

### align-items 定义项目在交叉轴如何对齐
{%codeblock%}
.box{
    align-items: flex-start | flex-end | center | baseline | strech ;
}
{%endcodeblock%}

它有5个值
{%codeblock%}

flex-start：交叉轴的起点对齐。

flex-end：交叉轴的终点对齐。

center：交叉轴的中点对齐。

baseline: 项目的第一行文字的基线对齐。

stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

{%endcodeblock%}

### align-content 定义多根轴线的对齐方式，如果改项目只有一个轴线，则该属性没有作用
{%codeblock%}
.box{
    align-content: flex-start | flex-end | center | strech | space-between | space-around
}
{%endcodeblock%}

它有5个值
{%codeblock%}

flex-start：与交叉轴的起点对齐。

flex-end：与交叉轴的终点对齐。

center：与交叉轴的中点对齐。

space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。

space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。

stretch（默认值）：轴线占满整个交叉轴。

{%endcodeblock%}

## 项目的6个属性
{%codeblock%}
order           //定义排列顺序，数值越小，排列越靠前
flex-grow       //定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
flex-shrink     //定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
flex-basis      //定义了在分配多余空间之前，项目占据的主轴空间
flex            //是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto
align-self      //允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto
{%endcodeblock%}


### order 定义排列
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
{%codeblock%}
.item {
  order: <integer>;
}
{%endcodeblock%}


### flex-grow属性
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大

{%codeblock%}

.item {
  flex-grow: <number>; /* default 0 */
}
{%endcodeblock%}

### flex-shrink属性
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

{%codeblock%}
.item {
  flex-shrink: <number>; /* default 1 */
}
{%endcodeblock%}

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
负值对该属性无效。

### flex-basis属性
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

{%codeblock%}
.item {
  flex-basis: <length> | auto; /* default auto */
}
{%endcodeblock%}

它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

### flex属性
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

{%codeblock%}
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
{%endcodeblock%}

该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。


### align-self属性
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

{%codeblock%}
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
{%endcodeblock%}

该属性可能取6个值，除了auto，其他都与align-items属性完全一致



原文地址http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html