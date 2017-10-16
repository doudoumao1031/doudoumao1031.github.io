---
layout:     post
title:      "gulp学习笔记"
subtitle:   "gulp,gulp-plugins,npm,cnpm"
date:       2017-10-16
author:     "doudoumao"
header-img: "img/post-bg-js-version.jpg"
tags:
    - 前端开发
    - JavaScript
---
![java-javascript](/img/in-post/post-gulp/gulp-logo-mini.png)
# The streaming build system
## What is gulp?
- Automation - gulp is a toolkit that helps you automate painful or time-consuming tasks in your development workflow.
- Platform-agnostic - Integrations are built into all major IDEs and people are using gulp with PHP, .NET, Node.js, Java, and other platforms.
- Strong Ecosystem - Use npm modules to do anything you want + over 2000 curated plugins for streaming file transformations
- Simple - By providing only a minimal API surface, gulp is easy to learn and simple to use

## npm介绍
##### 1、使用npm安装插件：命令提示符执行npm install <name> [-g] [--save-dev]；<br>
1.1、<name>：node插件名称。例：npm install gulp-less --save-dev	<br>
1.2、-g：全局安装。将会安装在C:\Users\Administrator\AppData\Roaming\npm，并且写入系统环境变量；  非全局安装：将会安装在当前定位目录；  全局安装可以通过命令行在任何地方调用它，本地安装将安装在定位目录的node_modules文件夹下，通过require()调用；<br>
1.3、--save：将保存配置信息至package.json（package.json是nodejs项目配置文件）；<br>
1.4、-dev：保存至package.json的devDependencies节点，不指定-dev将保存至dependencies节点；一般保存在dependencies的像这些express/ejs/body-parser等等。<br>
1.5、为什么要保存至package.json？因为node插件包相对来说非常庞大，所以不加入版本管理，将配置信息写入package.json并将其加入版本管理，其他开发者对应下载即可（命令提示符执行npm install，则会根据package.json下载所有需要的包，npm install --production只下载dependencies节点的包）。<br>
##### 2、使用npm卸载插件：npm uninstall <name> [-g] [--save-dev]  PS：不要直接删除本地插件包<br>
2.1、删除全部插件：npm uninstall gulp-less gulp-uglify gulp-concat ……???太麻烦<br>
2.2、借助rimraf：npm install rimraf -g 用法：rimraf node_modules<br>
##### 3、使用npm更新插件：npm update <name> [-g] [--save-dev]<br>
3.1、更新全部插件：npm update [--save-dev]
##### 4、查看npm帮助：npm help
##### 5、当前目录已安装插件：npm list
##### 6、选装cnpm<br>
6.1、官方网址：http://npm.taobao.org；<br>
6.2、安装：命令提示符执行npm install cnpm -g --registry=https://registry.npm.taobao.org；  注意：安装完后最好查看其版本号cnpm -v或关闭命令提示符重新打开，安装完直接使用有可能会出现错误；
注：cnpm跟npm用法完全一致，只是在执行命令时将npm改为cnpm（以下操作将以cnpm代替npm）。

