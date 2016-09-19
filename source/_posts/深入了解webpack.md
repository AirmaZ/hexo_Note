---
title: 深入了解webpack
date: 2016-09-19 14:55:26
tags: webpack
categories: react
---

## 前言 ##
webpack是近期最火的一款模块加载器兼打包工具，它能把各种资源，例如JS（含JSX）、coffee、样式（含less/sass）、图片等都作为模块来使用和处理。

当前现在网上也有很多webpack的讲解，但都是些傻瓜式的配置教程，没有对webpack其中`webpack.config.js`中的字段进行详细的解释，以至于很多同学只是会只用别人配置好的项目，没有独立diy的能力。所以本文将从webpack的安装、核心原理、功能说明、配置字段解析这几个大方向来教大家学会如何使用webpack。

## Webpack安装 ##

1. Webpack很多功能都依赖于node.js环境，所以在使用webpack前你的电脑上必须要有node.js+npm，至于这两者如何安装配置我就不说了，不在本文讨论范围内，网上有很多现成的教学。
2. 安装分为全局安装和非全局，我们建议非全局安装的方式
  - 全局：我们常规直接使用 npm 的形式来安装Webpack：`$ npm install webpack -g`
  - 非全局：正常情况下我们都会将依赖写入`package.json`，然后执行初始化命令：`$ npm init`，安装webpack：`$ npm install webpack --save-dev`。

## Webpack核心原理 ##

webpack有两大核心原理：
1. 一切皆模块
正如js文件可以是一个“模块（module）”一样，其他的（如css、image或html）文件也可视作模 块。因此，你可以`require('myJSfile.js')`亦可以`require('myCSSfile.css')`。这意味着我们可以将事物（业务）分割成更小的易于管理的片段，从而达到重复利用等的目的。
2. 按需加载
传统的模块打包工具（module bundlers）最终将所有的模块编译生成一个庞大的bundle.js文件。但是在真实的app里边，“bundle.js”文件可能有10M到15M之大可能会导致应用一直处于加载中状态。因此Webpack使用许多特性来分割代码然后生成多个“bundle”文件，而且异步加载部分代码以实现按需加载。

## webpack功能 ##

### 1.开发模式和生产模式 ###
首先要知道的是Webpack有许许多多的特性，一些是”开发模式“下才有的，一些是”生产模式“下才有的，还有一些是两种模式下都有的：

![开发模式和生产模式](http://i.imgur.com/AMYCGhZ.png)

例如：
> 为了生成bundles文件你可能在package.json文件加入如下的scripts项：
```
"scripts": {
  // 运行npm run build 来编译生成生产模式下的bundles
  "build": "webpack --config webpack.config.prod.js",
  // 运行npm run dev来生成开发模式下的bundles以及启动本地server
  "dev": "webpack-dev-server"
 }
```

### 2.webpack CLI 和webpack-dev-server ###
Webpack为用户提供两种交互接口：
1. Webpack CLI tool：默认的交互方式（已随Webpack本身安装到本地）
2. webpack-dev-server：一个Node.js服务器（需要开发者从npm自行安装）

##### *Webpack CLI（有利于生产模式下打包）* #####
用法：
```
方式1: 
// 全局模式安装webpack
npm install webpack --g
// 在终端输入
$ webpack // <--使用webpack.config.js生成bundle
方式 2 :
// 非全局模式安装webpack然后添加到package.json依赖里边
npm install webpack --save
// 添加build命令到package.json的scripts配置项
"scripts": {
 "build": "webpack --config webpack.config.prod.js -p",
 ...
 }
// 用法：
"npm run build"
```

##### *webpack-dev-server（有利于在开发模式下编译）* #####
这是一个基于Express.js框架开发的web server，默认监听8080端口。server内部调用Webpack，这样做的好处是提供了额外的功能如热更新“Live Reload”以及热替换“Hot Module Replacement”（即HMR）。

1. 用法：
```
方式 1:
// 全局安装
npm install webpack-dev-server --save
// 终端输入
$ webpack-dev-server --inline --hot
用法 2:
// 添加到package.json scripts
"scripts": {
 "start": "webpack-dev-server --inline --hot",
 ...
 }
// 运行： 
$ npm start
// 浏览器预览：
http://localhost:8080
```

2. “hot” 和 “inline”功能：
“inline”选项会为入口页面添加“热加载”功能，“hot”选项则开启“热替换（Hot Module Reloading）”，即尝试重新加载组件改变的部分（而不是重新加载整个页面）。如果两个参数都传入，当资源改变时，webpack-dev-server将会先尝试HRM（即热替换），如果失败则重新加载整个入口页面。
```
// 通过CLI传参
webpack-dev-server --hot --inline
// 通过webpack.config.js传参
devServer: {
  inline: true,
  hot:true
}
```

## 相关配置字段解析 ##

### 1.entry ###
Enter配置项告诉Webpack应用的根模块或起始点在哪里，它的值可以是字符串、数组或对象。这看起来可能令人困惑，因为不同类型的值有着不同的目的。

像绝大多数app一样，倘若你的应用只有一个单一的入口，enter项的值你可以使用任意类型，最终输出的结果都是一样的。

##### *enter：数组类型* #####
你想添加多个彼此不互相依赖的文件，你可以使用数组格式的值。例如，你可能在html文件里引用了“googleAnalytics.js”文件，可以告诉Webpack将其加到bundle.js的最后。
![](http://i.imgur.com/sk32RvT.png)

##### *enter：对象* #####
现在，假设你的应用是多页面的（multi-page application）而不是SPA，有多个html文件（index.html和profile.html）。然后你通过一个对象告诉Webpack为每一个html生成一个bundle文件。

以下的配置将会生成两个js文件：indexEntry.js和profileEntry.js分别会在index.html和profile.html中被引用。
![](http://i.imgur.com/U1f6dJ4.png)

##### *enter：混合类型* #####
你也可以在enter将数组对象混用。例如下面的配置将会生成3个文件：vender.js（包含三个文件），index.js和profile.js文件。
![](http://i.imgur.com/bY9wAv3.png)

### 2.output ###
output项告诉webpack怎样存储输出结果以及存储到哪里。output的两个配置项“path”和“publicPath”可能会给大家造成困惑。

“path”仅仅告诉Webpack结果存储在哪里，然而“publicPath”项则被许多Webpack的插件用于在生产模式下更新内嵌到css、html文件里的url值。
![](http://i.imgur.com/JHRGPnt.png)

例如，在localhost里的css文件中边你可能用“./test.png”这样的url来加载图片，但是在生产模式下“test.png”文件可能会定位到CDN上并且你的Node.js服务器可能是运行在HeroKu上边的。这就意味着在生产环境你必须手动更新所有文件里的url为CDN的路径。

然而你也可以使用Webpack的“publicPath”选项和一些插件来在生产模式下编译输出文件时自动更新这些url。
![](http://i.imgur.com/pQJGrEz.png)
```
// 开发环境：Server和图片都是在localhost（域名）下
.image { 
  background-image: url('./test.png');
 }
// 生产环境：Server部署下HeroKu但是图片在CDN上
.image { 
  background-image: url('https://someCDN/test.png');
 }
```

### 3.module & loaders ###


##### *module* #####
模块加载器是可自由添加的Node模块，用于将不同类型的文件“load”或“import”并转换成浏览器可以识别的类型，如js、Stylesheet等。更高级的模块加载器甚至可以支持使用ES6里边的“require”或“import”引入模块。

例如，你可以使用babel-loader来将使用ES6语法写成的文件转换成ES5：
```
module: {
 loaders: [{
  test: /\.js$/, // 匹配.js文件，如果通过则使用下面的loader
  exclude: /node_modules/, // 排除node_modules文件夹
  loader: 'babel' // 使用babel（babel-loader的简写）作为loader
 }]
```

##### *loaders* #####
loaders意为“加载器”，区分于plugins“插件”。
+ 链式的加载器（从右往左执行）
多个loader可以用在同一个文件上并且被链式调用。链式调用时从右到左执行且loader之间用“!”来分割。
例如，假设我们有一个名为“myCssFile.css”的css文件，然后我们想将它的内容使用style标签内联到最终输出的html里边。我们可以使用css-loader和style-loader两个loader来达到目的。
```
module: {
 loaders: [{
  test: /\.css$/,
  loader: 'style!css' //(short for style-loader!css-loader)
 }]
```
+ loader自身可以配置
模块加载器（loader）自身可以根据传入不同的参数进行配置。
在下面的例子中，我们可以配置url-loader来将小于1024字节的图片使用DataUrl替换而大于1024字节的图片使用url，我们可以用如下两种方式通过传入“limit“参数来实现这一目的：
![](http://i.imgur.com/tBdakXB.png)

### 4.plugins ###
插件一般都是用于输出bundle的node模块。
例如，uglifyJSPlugin获取bundle.js然后压缩和混淆内容以减小文件体积。
类似的extract-text-webpack-plugin内部使用css-loader和style-loader来收集所有的css到一个地方最终将结果提取结果到一个独立的”styles.css“文件，并且在html里边引用style.css文件。
```
//webpack.config.js
// 获取所有的.css文件，合并它们的内容然后提取css内容到一个独立的”styles.css“里
var ETP = require("extract-text-webpack-plugin");
module: {
 loaders: [
  {test: /\.css$/, loader:ETP.extract("style-loader","css-loader") }
  ]
},
plugins: [
    new ExtractTextPlugin("styles.css") //Extract to styles.css file
  ]
}
```

### 5.resolve ###
很多Webpack的配置文件都有一个resolve属性，然后就像下面代码所示有一个空字符串的值。空字符串在此是为了resolve一些在import文件时不带文件扩展名的表达式，如`require('./myJSFile')`或者`import myJSFile from './myJSFile'`（注：实际就是自动添加后缀，默认是当成js文件来查找路径）
```
{
 resolve: {
   extensions: ['', '.js', '.jsx']
 }
}
```

## 结束 ##