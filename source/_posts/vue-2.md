---
title: vue组件及模板指令
date: 2017-09-22 17:02:45
tags: [vue]
categories: [编程]
---

### vue组件的重要选项

1.一个简单的实例
{%codeblock%}
#Hello world
    <div id="app">
        {{ message }}
    </div>

{%endcodeblock%}
{%codeblock%}
new Vue({
    el: '#app',
    date: {
        message: 'Hello Vue.js'
    }
})
{%endcodeblock%}
div 的id对应着el里的#app
message对应着data里的 "Hello Vue.js"

### data
{%codeblock%}
new Vue({
    a: 1,
    b: []
    }
})
{%endcodeblock%}
{%codeblock%}
<p>&#123;&#123;a&#125;&#125;</p>
{%endcodeblock%}
视图的p标签里对应着data 里面的数据a

### methods
{%codeblock%}
new Vue({
    data: {
        a: 1,
        b: []
    },
    methods: {
        doSomething: function (){
            console.log(this.a)
        }
    }
})
{%endcodeblock%}
### watch 
{%codeblock%}
new Vue({
    data: {
        a: 1,
        b: []
    },
    methods:{
        doSomething: function (){
            this.a ++
        }
    },
    watch: {
        'a': function(val,oldVal){
            console.log(val,oldVal)
        }
    }
})
{%endcodeblock%}


### 模版指令——html和vue对象的粘合剂

数据渲染：v-text、v-html、&#123;&#123;&#125;&#125;
{%codeblock%}
<p>{{a}}</p>
<p v-text='a'></p>
<p v-html='a'></p>


new Vue({
    data: {
        a: 1,
        b: []
    }
})
{%endcodeblock%}

### 模版指令——v-if  v-show

控制模块隐藏：v-if、v-show
{%codeblock%}
<p v-if="isShow"></p>
<p v-show="isShow"></p>


new Vue({
    data: {
        isShow: true;
    }
})
{%endcodeblock%}


### 模版指令 —— v-for
渲染循环列表：v-for 
{%codeblock%}
<ul>
    <li v-for="item in items">
        <p v-text="item.label"></p>
    </li>
</ul>


new Vue({
    data: {
        items: [
            {
                lable: "apple"
            },
            {
                lable: "banana"
            }
        ]
    }
})
{%endcodeblock%}

### 模版指令——v-on  事件绑定

事件绑定：v-on

{%codeblock%}
<button v-on="doThis"></botton>
<button @click="doThis"></button>


new Vue({
    methods: {
        doThis: function(something){

        }
    }
}
{%endcodeblock%}


### 模版指令——v-bind

属性绑定：v-bind
{%codeblock%}
<img v-bind:src="imgageSrc"/>

<div :class="{ red: isRed }"></div>
<div :class="[classA,classB]"></div>
<div :class="[classA,{ classB: isB,classC: isC}]">
{%endcodeblock%}

### 小结
1.new一个vue对象的时候你可以设置它的属性，其中最重要的三个，分别是data,methods,watch.
2.其中data代表vue对象的数据，methods代表vue对象的方法，watch设置了对象监听的方法。
3.Vue对象里的设置通过html指令进行关联

### 重要的指令包括
    － v-text 渲染数据
    － v-if  控制显示
    － v-on  绑定事件
    - v-for  循环渲染等