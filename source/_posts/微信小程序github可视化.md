---
title: 微信小程序github可视化
date: 2018-09-07 12:37:40
tags:
---

### 前言
一直想做一些数据可视化的东西，所以就尝试在微信小程序中获取用户的一些GitHub上的数据以后，使用[wx-charts](https://github.com/xiaolin3303/wx-charts)来进行开发，GitHub的api可参考[GitHubApi](https://segmentfault.com/a/1190000015144126)，目前只是获取了数据暂时展示了一下，样式请忽略😁，项目持续更新。
### 完成
暂时完成了：  
18/09/06
* following
* follows
* repositories和starts
* 仓库的语言类型  

18/09/07
* 返回重输
* 输入为空和成功的优化
* 点击跟随人跳转进相应人信息
* 点击环形图弹出对应信息
### 预览

[git地址](https://github.com/lucaswww/wx-gitinfo)

![](https://user-gold-cdn.xitu.io/2018/9/7/165b24bf9e8c67fd?w=425&h=746&f=gif&s=998855)
### 所用
[wx-charts](https://github.com/xiaolin3303/wx-charts)：去[这里](https://github.com/xiaolin3303/wx-charts/blob/master/dist/wxcharts.js)直接复制到你的项目随便哪里，在需要引用的地方 `var wxCharts = require('../../utils/wxcharts.js');` ，例子都在他[官网](https://github.com/xiaolin3303/wx-charts-demo),需要下载到小程序中看效果，这里就展示一个饼图的基本代码：  
index.wxml:
```
  <view>
    <canvas canvas-id="pieCanvas" class="canvas" style="height:300px;width:100%;"></canvas>
  </view>
```
index.js
```
var windowWidth = 320;
try {
  var res = wx.getSystemInfoSync();
  windowWidth = res.windowWidth;
} catch (e) {
  console.error('getSystemInfoSync failed!');
}
new wxCharts({
  animation: true,
  canvasId: 'pieCanvas',
  type: 'pie',
  series: [{
    name: 'javascript',
    data: 3
  }, {
    name: 'java',
    data: 1
  }, {
    name: 'vue',
    data: 6
  }],
  width: windowWidth,
  height: 300,
  dataLabel: true,
})
```
效果：
![](https://user-gold-cdn.xitu.io/2018/9/6/165aef0156f40807?w=264&h=284&f=png&s=10629)  
[GitHubApi](https://segmentfault.com/a/1190000015144126)：这里别人总结的github的api的一些用法，感谢！（api的请求次数有限制，如果自己在开发时需要经常请求，可以把一次请求的数据暂时存起来）  
weui-wexx：去[这里](https://github.com/Tencent/weui-wxss/blob/master/dist/style/weui.wxss)直接复制到你的项目根目录下取名weui.wxss，然后在app.wxss中 `@import 'weui.wxss'`就好了，具体使用还是要去看他的[官网](https://github.com/Tencent/weui-wxss)
