---
title: FLEX布局探索
date: 2016-09-20 15:12:51
tags: CSS
categories: CSS
---

## 前言 ##

以前布局采用的解决方案都是css盒模型布局，其中包涵了各种奇怪的技巧，例如不定高的盒子居中等等不容易实现，而flex布局可以轻易实现我们以前需要大费周章的布局需求。

在兼容性上，flex目前已经支持了所有的浏览器（IE 10+,chrome 21+，firefox 22+等），可以说是日后主流的布局解决方案。不过使用flex布局后，会导致一些冲突的css失效。

## container和items ##

在flex中，设置了`display：flex；`的容器将作为flex项目容器，我叫它container，而container中的子容器我称它们为item。item也可以设置`display：flex`来作为container形成嵌套。

<!--more-->

#### container相关属性 ####

+ flex-direction （items的排列方向）
+ flex-wrap （items的换行方式）
+ flex-flow （flex-direction和flex-wrap的缩写）
+ justify-content （主轴对齐方式）
+ align-items （items交叉轴对齐方式）
+ align-content （多轴线对齐方式）

#### items相关属性 ####

+ order (自身的排序)
+ flex-grow （自身的放大比例）
+ flex-shrink （自身的缩小比例）
+ flex-basis （占用主轴的空间）
+ flex （“grow”、“shrink”、“basis”的缩写）
+ align-self （单独定义的交叉轴对齐方式）

## 基于FLEX的响应式布局 ##

#### 效果图 ####
![桌面端](http://i.imgur.com/cwPZdIU.jpg)
![移动端](http://i.imgur.com/LTHqFPi.jpg)

#### HTML代码 ####

```html
<div class="container">
     <header class="header"></header>
     <div class="body">
         <div class="left"></div>
         <div class="content"></div>
         <div class="right"></div>
     </div>
     <div class="footer"></div>
 </div>
```

#### CSS代码 ####
```css
.container{
    background-color: cadetblue;
    box-shadow: 2px 2px 10px black;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: flex-start;
    width: 100%;
    height: 600px;
    border-radius: 20px;
    overflow: hidden;
}

.header{
    width: 100%;
    height: 10%;
    background-color: #b44141;
}
.body{
    width: 100%;
    height: 80%;
    background-color: #6a8759;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    padding: 10px;
}
.footer{
    width: 100%;
    height: 10%;
    background-color: #94972e;
}
@media (min-width: 769px) {
    .left{
        flex-grow: 1;
        background-color: #204040;
        height: 100%;
    }
    .content{
        flex-grow: 5;
        background-color: #afafaf;
        height: 100%;
        margin: 10px;
    }
    .right{
        flex-grow: 1;
        background-color: #204040;
        height: 100%;
    }
}
@media (max-width: 768px) {
    .left{
        order: 1;
        width: 100%;
        height: 10%;
        background-color: #94972e;
    }
    .content{
        order: 2;
        width: 100%;
        height: 80%;
        background-color: #afafaf;
    }
    .right{
        order: 1;
        width: 100%;
        height: 10%;
        background-color: #204040;
    }
}
```

## 未完待续 ##