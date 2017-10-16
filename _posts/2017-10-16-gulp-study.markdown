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

## npm介绍：
###### 1、使用npm安装插件：命令提示符执行npm install <name> [-g] [--save-dev]；<br>
&emsp;&emsp; 1.1、<name>：node插件名称。例：npm install gulp-less --save-dev	<br>
&emsp;&emsp; 1.2、-g：全局安装。将会安装在C:\Users\Administrator\AppData\Roaming\npm，并且写入系统环境变量；  非全局安装：将会安装在当前定位目录；  全局安装可以通过命令行在任何地方调用它，本地安装将安装在定位目录的node_modules文件夹下，通过require()调用；<br>
&emsp;&emsp; 1.3、--save：将保存配置信息至package.json（package.json是nodejs项目配置文件）；<br>
&emsp;&emsp; 1.4、-dev：保存至package.json的devDependencies节点，不指定-dev将保存至dependencies节点；一般保存在dependencies的像这些express/ejs/body-parser等等。<br>
&emsp;&emsp; 1.5、为什么要保存至package.json？因为node插件包相对来说非常庞大，所以不加入版本管理，将配置信息写入package.json并将其加入版本管理，其他开发者对应下载即可（命令提示符执行npm install，则会根据package.json下载所有需要的包，npm install --production只下载dependencies节点的包）。<br>
###### 2、使用npm卸载插件：npm uninstall <name> [-g] [--save-dev]  PS：不要直接删除本地插件包<br>
&emsp;&emsp; 2.1、删除全部插件：npm uninstall gulp-less gulp-uglify gulp-concat ……???太麻烦<br>
&emsp;&emsp; 2.2、借助rimraf：npm install rimraf -g 用法：rimraf node_modules<br>
###### 3、使用npm更新插件：npm update <name> [-g] [--save-dev]<br>
&emsp;&emsp; 3.1、更新全部插件：npm update [--save-dev]
###### 4、查看npm帮助：npm help
###### 5、当前目录已安装插件：npm list
###### 6、选装cnpm<br>
&emsp;&emsp; 6.1、官方网址：http://npm.taobao.org；<br>
&emsp;&emsp; 6.2、安装：命令提示符执行npm install cnpm -g --registry=https://registry.npm.taobao.org；  注意：安装完后最好查看其版本号cnpm -v或关闭命令提示符重新打开，安装完直接使用有可能会出现错误；
注：cnpm跟npm用法完全一致，只是在执行命令时将npm改为cnpm（以下操作将以cnpm代替npm）。
###### 7、生成paskage.json: npm init PS:package.json是一个普通json文件，所以不能添加任何注释。	*（json不能加注释）*

## gulp：
###### 1、gulp安装
&emsp;&emsp; 全局安装了gulp，项目也安装了gulp，全局安装gulp是为了执行gulp任务，本地安装gulp则是为了调用gulp插件的功能。 PS：通过require()调用。
###### 2、gulpfile.js文件:
	//导入工具包 require('node_modules里对应模块')
	var gulp = require('gulp'), //本地安装gulp所用到的地方
    less = require('gulp-less');
 
	//定义一个testLess任务（自定义任务名称）
	gulp.task('testLess', function () {
    gulp.src('src/less/index.less') //该任务针对的文件
        .pipe(less()) //该任务调用的模块
        .pipe(gulp.dest('src/css')); //将会在src/css下生成index.css
	});
 
	gulp.task('default',['testLess', 'elseTask']); //定义默认任务 elseTask为其他任务，该示例没有定义elseTask任务
 
	//gulp.task(name[, deps], fn) 定义任务  name：任务名称 deps：依赖任务名称 fn：回调函数
	//gulp.src(globs[, options]) 执行任务处理的文件  globs：处理的文件路径(字符串或者字符串数组) 
	//gulp.dest(path[, options]) 处理完后文件生成路径

###### 3、使用webstorm运行gulp任务:<br>
右键gulpfile.js 选择”Show Gulp Tasks”打开Gulp窗口，若出现”No task found”，选择右键”Reload tasks”，双击运行即可。


## gulp APIs:


###### 1、gulp.task(name[, deps], fn)
说明：task定义一个gulp任务；<br>
name：  类型(必填)：String 指定任务的名称（不应该有空格）；<br>
deps：  类型(可选)：StringArray，该任务依赖的任务*（注意：被依赖的任务需要返回当前任务的事件流，请参看下面示例）*<br>
fn：  类型(必填)：Function 该任务调用的插件操作；

	gulp.task('testLess', function () {
    return gulp.src(['less/style.less'])
        .pipe(less())
        .pipe(gulp.dest('./css'));
	});
 
	gulp.task('minicss', ['testLess'], function () { //执行完testLess任务后再执行minicss任务
    gulp.src(['css/*.css'])
        .pipe(minifyCss())
        .pipe(gulp.dest('./dist/css'));
	});


###### 2、gulp.src(globs[, options])
说明：src方法是指定需要处理的源文件的路径，gulp借鉴了Unix操作系统的管道（pipe）思想，**前一级的输出，直接变成后一级的输入，**gulp.src返回当前文件流至可用插件；<br>

globs：  需要处理的源文件匹配符路径。类型(必填)：String or StringArray；<br>
通配符路径匹配示例：<br>
>“src/a.js”：指定具体文件；<br>
“*”：匹配所有文件    例：src/*.js(包含src下的所有js文件)；<br>
“**”：匹配0个或多个子文件夹    例：src/**/*.js(包含src的0个或多个子文件夹下的js文件)；<br>
“{}”：匹配多个属性    例：src/{a,b}.js(包含a.js和b.js文件)  src/*.{jpg,png,gif}(src下的所有jpg/png/gif文件)；<br>
“!”：排除文件    例：!src/a.js(不包含src下的a.js文件)；

	var gulp = require('gulp'),
    less = require('gulp-less');
 
	gulp.task('testLess', function () {
    //gulp.src('less/test/style.less')
    gulp.src(['less/**/*.less','!less/{extend,page}/*.less'])
        .pipe(less())
        .pipe(gulp.dest('./css'));
	});
options：  类型(可选)：Object，有3个属性buffer、read、base；
options.buffer：  类型：Boolean  默认：true 设置为false，将返回file.content的流并且不缓冲文件，处理大文件时非常有用；
options.read：  类型：Boolean  默认：true 设置false，将不执行读取文件操作，返回null；
options.base：  类型：String  设置输出路径以某个路径的某个组成部分为基础向后拼接，具体看下面示例：
	
	gulp.src('client/js/**/*.js')
		.pipe(minify())
		.pipe(gulp.dest('build'));  // Writes 'build/somedir/somefile.js'
 
	gulp.src('client/js/**/*.js', { base: 'client' })
		.pipe(minify())
		.pipe(gulp.dest('build'));  // Writes 'build/js/somedir/somefile.js'


###### 3、gulp.dest(path[, options])
说明：dest方法是指定处理完后文件输出的路径；

	gulp.src('./client/templates/*.jade')
		.pipe(jade())
		.pipe(gulp.dest('./build/templates'))
		.pipe(minify())
		.pipe(gulp.dest('./build/minified_templates'));

path：  类型(必填)：String or Function 指定文件输出路径，**或者定义函数返回文件输出路径亦可；**<br>
options：  类型(可选)：Object，有2个属性cwd、mode；<br>
options.cwd：  类型：String  默认：process.cwd()：前脚本的工作目录的路径 当文件输出路径为相对路径将会用到；<br>
options.mode：  类型：String  默认：0777 指定被创建文件夹的权限；<br>

###### 4、gulp.watch(glob [, opts], tasks) or gulp.watch(glob [, opts, cb])
说明：watch方法是用于监听文件变化，文件一修改就会执行指定的任务；<br>
glob：  需要处理的源文件匹配符路径。类型(必填)：String or StringArray；<br>
opts：  类型(可选)：Object 具体参看https://github.com/shama/gaze；<br>
tasks：  类型(必填)：StringArray 需要执行的任务的名称数组；<br>
cb(event)：  类型(可选)：Function 每个文件变化执行的回调函数；<br>

	gulp.task('watch1', function () {
    	gulp.watch('less/**/*.less', ['testLess']);
	});
 
	gulp.task('watch2', function () {
    	gulp.watch('js/**/*.js', function (event) {
        	console.log('File ' + event.path + ' was ' + event.type + ', running tasks...');
    	});
	});