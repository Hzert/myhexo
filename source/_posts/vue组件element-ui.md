---
title: vue组件element-ui
date: 2017-09-29 13:11:57
tags: [vue]
categories: [编程]
---
## 安装element-ui
{%codeblock%}
npm i element-ui@1.0.9  //@后接版本号
建议固定vue和element-ui版本，避免版本升级产生冲突
{%endcodeblock%}


## 引入element-ui
在App.vue引入element-ui，然后就可以在其他任何页面中使用了
{%codeblock%}
import Element from "element-ui"
import 'element-ui/lib/theme-default/index.css'
Vue.use(Element)
{%endcodeblock%}

## 使用element-ui
{%codeblock%}
<template>
      <div id="app">
        <!-- 头部导航 -->
        <header class="header">
        <el-row>
            <el-col :span="24">
              <el-menu default-active="5" class="el-menu-demo" mode="horizontal" @select="">
                <el-menu-item index="1">高级插件</el-menu-item>
                <el-menu-item index="2">在线商城</el-menu-item>
                <el-menu-item index="3">客户管理</el-menu-item>
                <el-menu-item index="4">系统设置</el-menu-item>
                <el-menu-item index="5">活动发布</el-menu-item>
              </el-menu>
            </el-col>
        </el-row>
        </header>
        <div style="position: relative;height: 60px;width: 100%;"></div>

        <main>
              <!-- 左侧导航 -->
            <div class="main-left">
              <el-menu default-active="/activePublic" class="el-menu-vertical-demo" :router="true">
                <el-menu-item index="/page" :class="{'isActive': active}"><i class="el-icon-message"></i>活动发布</el-menu-item>
                <el-menu-item index="/" :class="{'isActive': !active}"><i class="el-icon-message"></i>活动管理</el-menu-item>
              </el-menu>
            </div>

              <!-- 右侧主内容区 -->
              <div  class="main-right" >
                  <router-view class="view"></router-view>
              </div>
        </main>
      </div>
    </template>

    <script>
    import Vue from 'vue'
    import Element from 'element-ui'
    import 'element-ui/lib/theme-default/index.css'

    Vue.use(Element)

    export default {
      name: 'app',
      data () {
        return {
          active: true
        }
      }
    }
    </script>

    <style>
      body{margin: 0;}
    #app {
      min-width: 1200px;
      margin: 0 auto;
      font-family: "Helvetica Neue","PingFang SC",Arial,sans-serif;
    }
    /* 头部导航 */
    header{z-index: 1000;min-width: 1200px;transition: all 0.5s ease;  border-top: solid 4px #3091F2;  background-color: #fff;  box-shadow: 0 2px 4px 0 rgba(0,0,0,.12),0 0 6px 0 rgba(0,0,0,.04);  }
    header.header-fixed{position: fixed;top: 0;left: 0;right: 0;}
    header .el-menu-demo{padding-left: 300px!important;}

    /* 主内容区 */
      main{    display: -webkit-box;  display: -ms-flexbox;  display: flex;  min-height: 800px;  border: solid 40px #E9ECF1;  background-color: #FCFCFC;  }
      main .main-left{text-align: center;width: 200px;float: left;}
      main .main-right{-webkit-box-flex: 1;  -ms-flex: 1;  flex: 1;  background-color: #fff; padding: 50px 70px; }
      main .el-menu{background-color: transparent!important;}
    </style>
{%endcodeblock%}

## 预览项目，看到如图
{%codeblock%}
npm run dev
{%endcodeblock%}

![首页](/img/index.png)