---
title: 利用inline-block完成垂直居中
date: 2016-09-21 17:41:15
tags: CSS
categories: CSS
---

不定高元素垂直居中在盒模型解决方案中一直是个棘手的问题，比如采用负边距，或者translate来实现。刚发现通过将块级元素设置为inline-block也可以实现垂直居中，但只在position：relative下才有效，实用性不高，可以拿来研究或者娱乐下。

<!--more-->

## 代码 ##

我们先来放置几个高度不同DIV元素：
```html
 <div class="parent">
      <div class="child"></div>
      <div style="height:200px;" class="child"></div>
      <div style="height:300px;" class="child"></div>
      <div style="height:350px;" class="child"></div>
      <div style="height:400px;" class="child"></div>
    </div>
```

接下来设置CSS:
```css
      .parent{
        height: 400px;
        background: #265858;
        text-align: center;
      }
      .child{
        display: inline-block;
        vertical-align: middle;
        background: #ffde17;
        height: 100px;
        width: 100px;
      }
      .parent:after{
        content: '';
        display: inline-block;
        vertical-align: middle;
        height: 100%;
      }
```

## 效果图 ##
![](http://i.imgur.com/XSN3WKx.jpg)

## 原理猜测 ##
通过设置块级元素的display为inline-block可以让一个元素同时拥有块级元素和行内元素的特性。在展示上，拥有块级元素的特征，在文档流的行为中，却是行内元素。所以说设置了linline-block的块级元素可以使用vertical-align这个属性，用来模拟出行内元素的居中效果，同理，也可以设置为居顶部和居底部。

有的同学会问，这个after的作用是什么？

>我们先来去掉after试试：
>![](http://i.imgur.com/XSN3WKx.jpg)
>竟然没有任何作用，我们再来调低最后一个盒子的高度：
>![](http://i.imgur.com/t8zwBWs.jpg)
>这时候我们发现所有元素的居中基线变成了最高子元素的那个（也就是第四个黄色方块的中间位置），而after的作用正是设置了height：100%来强行撑开高度，让所有子元素以after为基线，至于为什么是这个样子，我并没有弄清楚。如果有人看到这篇文章，请留言告诉我谢谢。

## 结束 ##