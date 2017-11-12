---
layout:     post
title:      "Hybrid-app开发平台对比"
subtitle:   "Cordova,Mui/Dcloud,React Native"
date:       2017-11-13
author:     "Lee"
header-img: "img/post-bg-js-module.jpg"
tags:
    - 前端开发
    - JavaScript
---

## **混合开发四大平台:**##
- Cordova/PhoneGap 鼻祖 2011广泛流行，2012/12月开源
- AppCan 2012
- DCloud 2013
- APICloud 2014/9

**[CORDOVA/PHONEGAP](http://cordova.apache.org/)**

开发环境：安装原生开发环境，配置工程，使用HTML5、CSS3、js和原生SDK生成应用
<br>
加分：可以使用的框架、原生接口、支持平台都很多<br>
减分：在使用jQuery Mobile、Sencha Touch等前端框架的时候，有特效启动慢、页面切换慢、数据请求慢

**APPCAN**

appcan目前分两个版本：大众版、企业版。
<br>
大众版其实就是免费版，但功能有缺失（比如不能点对点推送、不能本地打包，必须上传到他们服务器植入他们自己的统计代码，否则打包出的app带有他们的水印）<br>
减分：闭源 优势不明显 性能不足以支撑大型app

**DCloud**

旗下四款产品：HBuilder、5+ Runtime、MUI、流应用都是弥补并扩展HTML5特性的产品。该公司的理念就是解决HTML5的性能、工具、能力三方面的问题。
<br>
MUI是一款不错的前端框架，性能比 jquery Mobile、Bootstrap好很多
<br>

- 设计思路不同，MUI坚持用原生JS做，不依赖jQuery或者Angularjs。<br>
- MUI调用了5+ Runtime（基于webview的增强runtime，扩展了大量的JS API，打通原生API和JS API的桥梁）的底层原生加速，比不带原生加速的框架更快。

>基本上总结起来一句话，就是多个 webview。在一些特定的地方，比如列表、下拉刷新，利用一些低版本 Android 上 webview 的滚动性能优于单个元素 overflow: scroll 的性能这一点，用多个 webview 来规避滚动性能问题。这个确实解决了国内 hybrid 开发的一些痛点

- MUI通过CSS动画、预加载、多个webview的显示隐藏等技术，比常规的纯webview还是好很多


加分：中国公司 文档,社区友好 学习成本低 性能相对较好
<br>
减分:新平台坑还较多

**APICloud**

性能无明显优势

APICloud提供原生应用的功能模块（设备访问，界面布局，开放SDK等），开发者可以通过JS调用。前端工程师负责页面布局，UI展现，及简单的交互，原生模块负责性能方面和功能实现，两者结合形成一个完整的应用。同时APICloud提供了云数据库的功能，前端不必了解PHP，Node.js等后端语言，通过JS接口或Restful API实现数据库的增删改查。

参考链接

- 对Cordova,APPCan,DCloud,APICloud四大平台的分析<br>[http://blog.csdn.net/tangzenglei/article/details/50668914](http://blog.csdn.net/tangzenglei/article/details/50668914)
- 如何评价DCloud？<br>[https://www.zhihu.com/question/31152731](https://www.zhihu.com/question/31152731)
- 国产框架MUI跟ReactNative的对比<br>[https://www.zhihu.com/question/39278015?sort=created](https://www.zhihu.com/question/39278015?sort=created)

总结：小体量APP（20w以内）个人倾向于使用DCloud

- 快速，开发成本低
- 社区友好，轮子多
- 引擎增强
- MUI比较轻
- 1次开发6端发布（h5浏览器,ios ipa,apk,微信app,百度直达号,流应用）

>hbuilder+mui+nativejs这套开发app，优点是入门容易，上手容易，熟悉后，开发app很快，而且大部分app都可以开发出来，只要不是有太多自定义动画的就好。也就是说找些刚毕业会写html js css的人就可以开发app，对比原生开发的价格，着实节省一大笔钱。性能问题，ios上很流畅，android这个趋势，千元机已经很牛逼了，所以也不需要太顾虑。


## **后起之秀：** ##

- React Native
- weex

RN与MUI的对比：

MUI：Webview至今无法过去的坎，那就是流畅性。不要再相信Webview能达到原生的性能，项目越大，页面越多，流程性越差，有天花板，优化的效果并不明显。稍微具有一定规模的项目，或者对流畅性要求较高的项目，建议不要用MUI。RN：学习成本和学习曲线还是比较高的，真的需要一段时间去学习。JSX看起来像JS，但是部分语法很奇葩。界面布局和CSS完全不一样，state和props相对还是比较好理解的，团队的学习成本更高。性能上可以说是完胜MUI。结论是：对流畅性要求不太高的，可以考虑MUI。开发速度快，成本低。对流程性要求高的，还是用RN吧。
