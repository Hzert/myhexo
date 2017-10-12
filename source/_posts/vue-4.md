---
title: vue组件开发~轮播图
date: 2017-09-28 09:25:31
tags: [vue]
categories: [编程]
---
## vue组件开发~轮播图

#### 主要用到的技术
    1.v-bind：属性绑定
    2.v-for：列表渲染
    3.v-show：条件渲染
    4.class的绑定切换
    5.created钩子
    6.Vue过渡效果

#### 步骤
##### 1.写好html和css
PS:这里和jQuery轮播图有所不同，因为Vue使用了列表渲染，所以只需要一个简单的结构的可以了

{%codeblock%}
<div class="carousel">
    <ul>
        <li>
            <a><img></a>
        </li>
    </ul>
    <div class="bullet">
        <span></span>
    </div>
{%endcodeblock%}

##### 2.初始化一个Vue实例，然后挂在父元素上去，并且设定数据为图片的数组，以及后面计数用的mark,mark的初始值为0

{%codeblock%}
new Vue({
    el: ".carousel",
    data: {
        mark: 0,
        img: [
            '../assets/imgs/pic.jpg',
            '../assets/imgs/pic1.jpg',
            '../assets/imgs/pic2.jpg',
        ]
    }
})
{%endcodeblock%}
貌似这种方法对于引用的vue.js 不适合搭建好的Vue,那解决办法如下：
{%codeblock%}
import pic from "../assets/imgs/pic.jpg"
import pic1 from "../assets/imgs/pic1.jpg"
import pic2 from "../assets/imgs/pic2.jpg"
import pic3 from "../assets/imgs/pic3.jpg"
export default {
    name: 'carousel',
    data () {
        return {
            mark: 0,
            img: [
                {imgurl:pic},
                {imgurl:pic1},
                {imgurl:pic2},
                {imgurl:pic3}
            ]
        }
        
    }
{%endcodeblock%}
利用import   export default

##### 3.分别在放置图片的li元素和放置选择标识的span元素中， 使用v-for遍历数据中的img属性和它的长度，
PS:在这里要注意的是，使用v-for循环的时候最好加上:key=标识。用以对后续对轮播图进行选择的标识
{%codeblock%}
<li v-for="(image,index) in img" :key='index'>
    <a><img></a>
</li>
v-for列表渲染
{%endcodeblock%}
{%codeblock%}
<div class="bullet">
    <span v-for='(item,index) in img-length' :class="{'active:index===mark'}" @click='change(index)' :key="index">
</div>

bullet渲染
{%endcodeblock%}

##### 4.使用v-bind的对img标签的src属性进行绑定，可以使用所写   :属性

{%codeblock%}
<a><img :src='image'></a>

使用v-bind绑定属性
{%endcodeblock%}

这时候轮播的效果和html结构是这样的，他还不会动以及切换图片。并且最后一张图在最上面（因为对li使用了position:absolute）

##### 5.现在来编写一下运行的逻辑
首先，1.当图片显示第几张的时候，下面的bullet的第几个就要标红，2.并且点击相应的bullet可以切换到对应的图片
1可以使用VUE的class绑定进行条件渲染，当标识index和图片的标识mark相等时就标红，2的话可以用vue的事件绑定v-on(我这里采用的时缩写@事件='执行的函数')对标识进行时间绑定

{%codeblock%}
<div class='bullet'>
    <span v-for='(item,index) in img.length' :class="{'active':index===mark}" @click="change(index)"></span>
</div>
{%endcodeblock%}

3.在vue实例中methods中添加change方法，change的实现很简单。直接将实例重点的data属性中的mark变为index的数字即可
{%codeblock%}
methods: {
    change(i){
        this.mark = i
    }
}
{%endcodeblock%}

4.使用v-show对li元素中显示的图片进行条件渲染，方法是当图片标识的index与vue实例中的mark相等时就显示该li元素
{%codeblock%}
<li v-for="(image,inde) in img" :key='index' v-show='index===mark'>
    <a><img :src='image'></a>
</li>
{%endcodeblock%}
这时候的vue轮播图就已经实现了点击下面的bullet标识切换图片的效果了。并且bullet标识也会有相应的标红
![](/img/vue-4.jpg)


#### ６．这时候的图片切换还没有平滑过度的效果，我们可以使用vue类名过方式对图片的切换添加过渡效果
![vue的类名过渡](https://cn.vuejs.org/v2/guide/transitions.html#%E8%BF%87%E6%B8%A1%E7%9A%84-CSS-%E7%B1%BB%E5%90%8D)
先要在需要过渡的元素的父元素，也就是ul元素中添加一个name属性，作为过渡效果类名的标记
{%codeblock%}
<ul class='clearfix slide' name="image">
    <li v-for='(image,inde) in img' :key='index' v-show="index===mark">
        <a><img :src='image'></a>
    </li>
</ul>
{%endcodeblock%}
然后在css中添加过渡效果的变化
{%codeblock%}
.image-enter-active {
        transform: translateX(0);
        transition: all 1s ease;
    }
    
    .image-leave-active {
        transform: translateX(-100%);
        transition: all 1s ease;
    }
    
    .image-enter {
        transform: translateX(100%)
    }
    
    .image-leave {
        transform: translateX(0)
    }
{%endcodeblock%}
最后将使用Vue中的过渡组件，将ul元素改为transition-group，然后添加tag属性，并且tag=ul（不添加的话ul元素名称显示为span元素）

{%codeblock%}
<transition-group class="clearfix slide" name='image'>
    <li v-for='(item,index) in img' :key="index" v-show="index===mark">
        <a href=""><img :src="item.imgurl" alt=""></a>
    </li>
</transition-group>
{%endcodeblock%}

#### 7.最后在methods中添加一个自动切换的函数，然后在created钩子函数中执行即可
{%codeblock%}
 created() {
        this.play()
    },
    methods: {
        change(i) {
            this.mark = i
        },
        autoPlay() {
            this.mark++
                if (this.mark === 4) {
                    this.mark = 0
                    return
                }
        },
        play() {
            setInterval(this.autoPlay, 3000)
        }
    }
{%endcodeblock%}