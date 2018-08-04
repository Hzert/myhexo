---
title: css技巧
date: 2017-11-02 11:20:27
tags: [css, 前端]
categories: [css]
---

## input radio   单选框，多选框 纯css实现的好看的样式

### css
{%codeblock%}
label {font-size:12px;cursor:pointer;}
label i {font-size:12px;font-style:normal;display:inline-block;width:12px;height:12px;text-align:center;line-height:12px;color:#fff;vertical-align:middle;margin:-2px 2px 1px 0px;border:#2489c5 1px solid;}
input[type="checkbox"],input[type="radio"] {display:none;}
input[type="radio"] + i {border-radius:7px;}
input[type="checkbox"]:checked + i,input[type="radio"]:checked + i {background:#2489c5;}
input[type="checkbox"]:disabled + i,input[type="radio"]:disabled + i {border-color:#ccc;}
input[type="checkbox"]:checked:disabled + i,input[type="radio"]:checked:disabled + i {background:#ccc;}
{%endcodeblock%}

### html
{%codeblock%}
<label><input type="checkbox"><i>✓</i>复选框</label><br>
<label><input type="checkbox" checked><i>✓</i>复选框</label><br>
<label><input type="checkbox" disabled><i>✓</i>复选框禁用</label><br>
<label><input type="checkbox" disabled checked><i>✓</i>复选框禁用已选</label><br>
<label><input type="radio" name="abc"><i>✓</i>单选框</label><br>
<label><input type="radio" name="abc" checked><i>✓</i>单选框</label><br>
<label><input type="radio" name="abc" disabled><i>✓</i>单选框禁用</label><br>
<label><input type="radio" name="def" disabled checked><i>✓</i>单选框禁用已选</label><br>
{%endcodeblock%}
![](/img/cssRadio.jpg)


## radio 的别的操作
{%codeblock%}
<style>
		
		.goods-info {
		  margin-top: 50px;
		  margin-bottom: 50px;
		}
		.goods-info .tag-label {
		  padding-top: 7px;
		}
		.goods-info .goods-tags {
		  margin-top: 2rem;
		}

		.tags-select {
		  font-size: 0;
		}
		.tags-select > .tag-select {
		  display: inline-block;
		  font-size: 14px;
		  margin: 5px;
		  position: relative;
		  font-weight: normal;
		}
		.tags-select > .tag-select .name {
		  display: block;
		  line-height: 20px;
		  padding: 8px 10px;
		  border: 1px solid #ccc;
		  cursor: pointer;
		}
		.tags-select > .tag-select input[type="radio"] {
		  position: absolute;
		  opacity: 0;
		  z-index: -1;
		}
		.tags-select > .tag-select input[type="radio"]:checked + .name {
		  border-color: #e3393c;
		}
		.tags-select > .tag-select input[type="radio"]:disabled + .name {
		  background: #eee;
		  color: #999;
		  cursor: not-allowed;
		}

	</style>
{%endcodeblock%}

{%codeblock%}
<div class="container goods-info">
  <div class="row goods-tags">
    <div class="col-md-2 tag-label">选择版本</div> 
    <div class="col-md-10">
      <div class="tags-select">
        <label class="tag-select">
          <input type="radio" name="version" value="1">
          <span class="name">全网通（2GB 16GB）</span>  
        </label>
        <label class="tag-select">
          <input type="radio" name="version" value="2">
          <span class="name">全网通（3GB 32GB）</span>  
        </label>  
        <label class="tag-select">
          <input type="radio" name="version" value="3" disabled>
          <span class="name">联通版（2GB 16GB）</span>  
        </label>  
      </div>  
    </div> 
  </div>
  <div class="row goods-tags">
    <div class="col-md-2 tag-label">购买方式</div> 
    <div class="col-md-10">
      <div class="tags-select">
        <label class="tag-select">
          <input type="radio" name="bye-type" value="1">
          <span class="name">官方标配</span>  
        </label>
        <label class="tag-select">
          <input type="radio" name="bye-type" value="2">
          <span class="name">移动优惠购</span>  
        </label>  
        <label class="tag-select">
          <input type="radio" name="bye-type" value="3" disabled>
          <span class="name">联通优惠购</span>  
        </label>  
        <label class="tag-select">
          <input type="radio" name="bye-type" value="4">
          <span class="name">电信优惠购</span>  
        </label>  
      </div>  
    </div> 
  </div>  
{%endcodeblock%}
![](/img/cssCode1.jpg)

## 垂直居中一个div中的图片
{%codeblock%}
<style>
		.vertical-container{
			height: 300px;
			display: flex;
			align-items: center;
			justify-content: center;
			border:1px solid yellow;
		}
		.vertical-container img{
			width:200px;
			height: 100px;
			border:1px solid red;
		}
	</style>

  <div class="vertical-container">
		<img src="">
	</div>

  重点在 align-items:center;
        justify-content:center
{%endcodeblock%}


### input 和span 同一行不对齐的情况。

解决方案：
{%codeblock%}
<div class="coverSearch">
  <span class="fl"><input type="text" class="searchSceneP" placeholder="场景包"></span>
  <span class="ScenePbtn btn-warning cursor"style="margin-left:0">查询</span>
</div>

就是在input 外面套一层span ，并让span 浮动
{%endcodeblock%}

## 一、左边固定，右边自适应的布局
{%codeblock%}
1. 左边左浮动，右边加个overflow:hidden;
   #lt{ float: left;width:200px; background: #ff0;}
   #rt{ overflow: hidden; background: #f0f;}

2. 左边左浮动，右边加个margin-left;
   #lt{ float: left; width:200px; background: #ff0;}
   #rt{ margin-left: 200px; background: #f0f;}

3. 左边绝对定位，右边加个margin-left;
   #lt{ position: absolute; top:0; left:0; width:200px; background: #ff0;}
   #rt{ margin-left: 200px; background: #f0f;}

4. 左右两边绝对定位，右边加个width,top,left,right
   #lt{ position: absolute; top:0 ; left:0 ;width:200px; background: #ff0;}
   #rt{ position: absolute; top:0 ; left:200px; width: 100% ; rigth:0;background: #f0f;}
{%endcodeblock%}

## 二、右边固定，左边自适应的布局
{%codeblock%}
1. 左边左浮动，margin-left负值,右边右浮动;
   #lt{float:left; width:100%;background: #00f;margin-right: -200px;}
   #rt{float: right; width: 200px;background: #ff0;}

2. 右边绝对定位，左边margin-right;
   #lt{margin-right:200px; background: #00f;}
   #rt{ position: absolute; right:0; top:0; width: 200px;background: #ff0;}

3. 左右两边绝对定位，左边加个width,top,left,right
   #lt{ position: absolute; top:0; left:0; rigth:0; width: 100% ; background: #f0f;}
   #rt{ position: absolute; top:0; left:200px; width:200px; background: #ff0;}
{%endcodeblock%}