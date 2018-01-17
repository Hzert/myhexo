---
title: vue初始项目发布到码云上的pages上可以直接访问！
date: 2018-01-11 15:20:54
tags: [vue,js]
categories: [编程,vue,javacript]
---
## 使用vue-cli构建一个新项目发布到gitee.com上并浏览
主要是想做一个自己的项目，然后还可以访问，之前有用hexo ＋ github pages 弄了一个博客，简单的博客，也就是现在这个，然后买了自己的域名，现在这个是想做一个其他的项目，为自己的简历加上一笔，然后目前选择的是gitee.com的一个pages服务，然后用了vue cli构建 ，慢慢学，慢慢做！
* * *
## 一，vue 项目创建
{%codeblock%}
//全局安装 vue-cli
npm install --global vue-cli
//创建一个基于webpack模版的新项目
vue init webpack newStart
// 安装依赖
cd newStart
npm install 
npm run dev
{%endcodeblock%}
npm run dev 以后可以直接浏览  localhost:8081 或者8080


## 二,vue 项目打包
 1. vue 打包的话，命令 npm run build 进行打包  然后会生成一个dist文件，里面有css ,js ,index.html
 如果要再gitee.com pages浏览的话，需要修改config/index.js里面的assetsPublicPath 改为./注意是再build下的，第一次我改的时候就改错了。


 ## 三，放到gitee.com上的pages服务上 
  1. 找到你再gitee.com上的新建的项目 找到pages服务
  2. 直接开启page服务 就会有一个网址出现，点击链接就可以看到你的网站了

##  四，用stylus编译css 
  1. pm install stylus --save-dev
  2. npm install stylus-loader --save-dev
  3. 然后就像下面代码一样可以使用了
{%codeblock%}
<style scoped lang="stylus">
h1
  font-size 20px
a
  border 1px solid #fff
</style>
{%endcodeblock%}

## 四, vue引入element-ui报错
vue引入elementUI 报错
在main.js里面引入import 'element-ui/lib/theme-default/index.css'中报错，无法启动项目，这是把package.json里面的webpack改成

1. "webpack": "beta",重新安装即可，这就可以启动了

2. elementUI 2.0版本的地址已经改为 'element-ui/lib/theme-chalk/index.css'，所以引入的的时候需要引入以下代码
{%codeblock%}
import 'element-ui/lib/theme-chalk/index.css'
{%endcodeblock%}


## 五，vuex 集中式状态管理架构,当项目大的时候，各个页面组件都要用到同一数据，属性就可以将这些属性设置为状态 
 1. 安装引入vuex
 {%codeblock%}
 npm install vuex --save 
 {%endcodeblock%}

 2. 新建一个vuex文件夹 并在文件夹下新建store.js文件，在文件中引入vue和vuex
 {%codeblock%}
 import Vue from "vue";
 import Vuex from "vuex";
 {%endcodeblock%}

 3. 使用vuex 引入之后用Vue.use进行引用
{%codeblock%}
Vue.use(Vuex);
{%endcodeblock%}
 
 4. vuex 里面用到的方法
{%codeblock%}

import Vue from 'vue';
import Vuex from 'vuex';
Vue.use(Vuex);
const state = {     // 状态对象
  count: 1
}

const mutations = {  // 修改状态 同步的
  add (state, n) {
    state.count += n;
  },
  reduce (state) {
    state.count--;
  }
}

const getters = {     // 计算过滤操作
  count: function (state) {
    return (state.count += 10);
  }
}

const actions = {
  addActions (context) {
    context.commit('add', 10);
    setTimeout(() => { context.commit('reduce') }, 3000);
  },
  reduceActions ({ commit }) {
    commit('reduce');
  }
}

export default new Vuex.Store({
  state,
  mutations,
  getters,
  actions
})

{%endcodeblock%}