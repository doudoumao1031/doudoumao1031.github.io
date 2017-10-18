---
layout:     post
title:      "gulp-plugins笔记"
subtitle:   "gulp,gulp-plugins,npm,cnpm"
date:       2017-10-17
author:     "doudoumao"
header-img: "img/post-bg-gulp1.jpg"
tags:
    - 前端开发
    - JavaScript
---
![gulp-logo](/img/in-post/post-gulp/gulp-logo-mini.png)
## gulp-htmlmin介绍：
* 安装：命令提示符执行 cnpm install gulp-htmlmin --save-dev<br>

![gulp-htmlmin-1](/img/in-post/post-gulp-plugins/gulp-htmlmin-1.png)

* 配置代码： 
		var gulp = require('gulp'),
		    htmlmin = require('gulp-htmlmin');
		 
		gulp.task('testHtmlmin', function () {
		    var options = {
		        removeComments: true,//清除HTML注释
		        collapseWhitespace: true,//压缩HTML
		        collapseBooleanAttributes: true,//省略布尔属性的值 <input checked="true"/> ==> <input />
		        removeEmptyAttributes: true,//删除所有空格作属性值 <input id="" /> ==> <input />
		        removeScriptTypeAttributes: true,//删除<script>的type="text/javascript"
		        removeStyleLinkTypeAttributes: true,//删除<style>和<link>的type="text/css"
		        minifyJS: true,//压缩页面JS
		        minifyCSS: true//压缩页面CSS
		    };
		    gulp.src('src/html/*.html')
		        .pipe(htmlmin(options))
		        .pipe(gulp.dest('dist/html'));
		});


## gulp-minify-css介绍：
* 安装：命令提示符执行 cnpm install gulp-minify-css --save-dev<br>

![gulp-htmlmin-1](/img/in-post/post-gulp-plugins/gulp-minify-css-1.png)

* 配置代码： 
		
		var gulp = require('gulp'),
		    cssmin = require('gulp-minify-css');
		 
		gulp.task('testCssmin', function () {
		    gulp.src('src/css/*.css')
		        .pipe(cssmin())
		        .pipe(gulp.dest('dist/css'));
		});