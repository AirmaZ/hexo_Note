---
title: Google前端代码规范(HTML/CSS)
date: 2016-09-19 17:30:23
tags: style
categories: other
---

## 目录 ##


+ [通用样式规则](#通用样式规则)
    - [协议](#协议)
+ [通用格式规则](#通用格式规则)
   - [缩进](#缩进)
   - [大写](#大写)
   - [尾部空白](#尾部空白)
+ [通用METE规则](#通用METE规则)
   - [编码](#编码)
   - [注释](#注释)
   - [代办项目](#代办项目)
+ [HTML样式规则](#HTML样式规则)
   - [DocumentType](#DocumentType)
   - [html的有效性](#html的有效性)
   - [媒体回退](#媒体回退)
   - [关注点分离](#关注点分离)
   - [实体引用](#实体引用)
   - [可选标签](#可选标签)
   - [type属性](#type属性)
+ [HTML格式规则](#HTML格式规则)
   - [通用格式](#通用格式)
   - [html中的引号](#html中的引号)
   - [css样式规则](#css样式规则)
   - [id和class的命名](#id和class的命名)
   - [id和class名称样式](#id和class名称样式)
   - [选择器](#选择器)
   - [简写属性](#简写属性)
   - [省略0后面的单位](#省略0后面的单位)
   - [第一位0省略](#第一位0省略)
   - [十六进制写法](#十六进制写法)
   - [命名前缀](#命名前缀)
   - [命名分隔符](#命名分隔符)
   - [hacks](#hacks)
+ [CSS格式规则](#CSS格式规则)
   - [书写顺序](#书写顺序)
   - [块内容的缩进](#块内容的缩进)
   - [分号停止声明](#分号停止声明)
   - [停止属性名称](#停止属性名称)
   - [块的分离](#块的分离)
   - [选择器的分离](#选择器的分离)
   - [规则的分离](#规则的分离)
   - [css引号](#css引号)

<!--more-->

----------


## 通用样式规则 ##
#### 协议 ####
> 省略协议部分(http、https)，再引入其他文件（图像、媒体文件等）一般省略其协议名称，除非相应的文件用了两个不同的协议。这样可以轻微的节省文件的大小，以及混淆代码所带来的一些问题。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;script src=&quot;https://www.google.com/js/gweb/analytics/autotrack.js&quot;&gt;&lt;/script&gt;
&lt;!-- 推荐 --&gt;
&lt;script src=&quot;//www.google.com/js/gweb/analytics/autotrack.js&quot;&gt;&lt;/script&gt;
/* 不推荐 */
.example {
  background: url(https://www.google.com/images/example);
}
/* 推荐 */
.example {
  background: url(//www.google.com/images/example);
}
</code></pre>

## 通用格式规则 ##
#### 缩进 ####
>通过两个空格来缩进，不推荐用制表符或者制表符空格混用的方式。
><pre><code>&lt;ul&gt;
  &lt;li&gt;Fantastic
  &lt;li&gt;Great
&lt;/ul&gt;
</code></pre><pre><code>
.example {
  color: blue;
}</code></pre>

#### 大写 ####
>仅仅使用小写字母,这包括：html的名称、属性、属性值（除非 text/CDATA），css选择器、属性、属性值等（除了一些字符串）
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;A HREF=&quot;/&quot;&gt;Home&lt;/A&gt;
&lt;!-- 推荐 --&gt;
&lt;img src=&quot;google.png&quot; alt=&quot;Google&quot;&gt;
/* 不推荐 */
color: #E5E5E5;
/* 推荐 */
color: #e5e5e5;</code></pre>


#### 尾部空白 ####
>不要再代码的尾部留空白，比如空格。这样会造成文件对比会比较复杂。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;p&gt;What?_
&lt;!-- 推荐 --&gt;
&lt;p&gt;Yes please.</code></pre>

## 通用METE规则 ##
#### 编码 ####
>一般使用UTF-8编码，通过`<meta charset="utf-8">`来设定编码，而不需要指定样式表的编码了。
>更多关于编码的使用请点击这里-->[https://www.w3.org/International/tutorials/tutorial-char-enc/](https://www.w3.org/International/tutorials/tutorial-char-enc/ "点我")

#### 注释 ####
>根据需要，或者说在大多数情况下，你都需要注释你的代码：解释代码段的目的，服务于那些内容，或者解释代码的使用方法等等。良好代码注释为别人带来更多的可读性。

#### 代办项目 ####
>使用关键字高亮的方式来标记一个ToDo，使用一个括号来标记一个联系人（姓名或者邮箱）。使用冒号来记录具体代码项目的内容：
><pre><code>{# TODO(john.doe): 重新测试 #}
&lt;center&gt;Test&lt;/center&gt;</code></pre><pre><code>
&lt;!-- TODO: 删除一些标签 --&gt;
&lt;ul&gt;
  &lt;li&gt;Apples&lt;/li&gt;
  &lt;li&gt;Oranges&lt;/li&gt;
&lt;/ul&gt;</code></pre>

## HTML样式规则 ##

#### Document Type ####
>推荐使用HTML5。使用`<!DOCTYPE html>`来进行声明。
>虽然我们推荐使用html，但是尽量不要使用XHTML，因为XHTML在浏览器的支持上并不友好。
>虽然无关HTML，但是建议尽量不要闭合空标签：书写`<br>`，而不是`<br/>`。

#### html的有效性 ####
>使用有效的html代码，除非一切特殊场合：模板等等。如果有必要，请使用一些工具来验证html的有效性比如[W3C HTML validator](https://validator.w3.org/nu/ " W3C HTML validator")
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;title&gt;Test&lt;/title&gt;
&lt;article&gt;This is only a test.</code></pre><pre><code>
&lt;!-- 推荐 --&gt;
&lt;!DOCTYPE html&gt;
&lt;meta charset=&quot;utf-8&quot;&gt;
&lt;title&gt;Test&lt;/title&gt;
&lt;article&gt;This is only a test.&lt;/article&gt;</code></pre>

#### 语义 ####
>如有可能请尽量使用带有语义的标签，如`<a>`表示一个链接，`<buttom>`表示一个按钮，而不是用没有语义的`<div>`去实现它们。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;div onclick=&quot;goToRecommendations();&quot;&gt;All recommendations&lt;/div&gt;
&lt;!-- 推荐 --&gt;
&lt;a href=&quot;recommendations/&quot;&gt;All recommendations&lt;/a&gt;</code></pre>

#### 媒体回退 ####
>对于多媒体的展示，如图像或者视频，请务必提供一些替代访问的内容（如alt），这将在用户无法显示你所给定媒体的时候告知用户这是哪方面的内容，在另一些场景中这将有助于盲人能够正常理解网页内容。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;img src=&quot;spreadsheet.png&quot;&gt;
&lt;!-- 推荐 --&gt;
&lt;img src=&quot;spreadsheet.png&quot; alt=&quot;Spreadsheet screenshot.&quot;&gt;</code></pre>

#### 关注点分离 ####
>严格遵守结构、样式、脚本分离的代码风格，并且试图让这三者之间的耦合性降低。也就是说一切的html尽量只服务于结构，而css只服务于展现样式，交互则交付于javascript。这样有利于增加代码的可读性，并且让代码的维护工作变得更加简单。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;!DOCTYPE html&gt;
&lt;title&gt;HTML sucks&lt;/title&gt;
&lt;link rel=&quot;stylesheet&quot; href=&quot;base.css&quot; media=&quot;screen&quot;&gt;
&lt;link rel=&quot;stylesheet&quot; href=&quot;grid.css&quot; media=&quot;screen&quot;&gt;
&lt;link rel=&quot;stylesheet&quot; href=&quot;print.css&quot; media=&quot;print&quot;&gt;
&lt;h1 style=&quot;font-size: 1em;&quot;&gt;HTML sucks&lt;/h1&gt;
&lt;p&gt;I’ve read about this on a few sites but now I’m sure:
  &lt;u&gt;HTML is stupid!!1&lt;/u&gt;
&lt;center&gt;I can’t believe there’s no way to control the styling of
  my website without doing everything all over again!&lt;/center&gt;</code></pre>
><pre><code>&lt;!-- 推荐 --&gt;
&lt;!DOCTYPE html&gt;
&lt;title&gt;My first CSS-only redesign&lt;/title&gt;
&lt;link rel=&quot;stylesheet&quot; href=&quot;default.css&quot;&gt;
&lt;h1&gt;My first CSS-only redesign&lt;/h1&gt;
&lt;p&gt;I’ve read about this on a few sites but today I’m actually
  doing it: separating concerns and avoiding anything in the HTML of
  my website that is presentational.
&lt;p&gt;It’s awesome!</code></pre>


#### 实体引用 ####
>如果你的项目或者团队之间用的都是“UTF-8”的编码，那么如果没有必要，则尽量不使用实体。除非一些拥有额外意义的符号，如`<`、`&`之类的。
><pre><code>&lt;!-- 不推荐 --&gt;
The currency symbol for the Euro is &amp;ldquo;&amp;eur;&amp;rdquo;.
&lt;!-- 推荐 --&gt;
The currency symbol for the Euro is “€”.</code></pre>

#### 可选标签 ####
>出于优化文件大小以及SEO优化的考虑，可以省略可选标签。你可以在[html5规范](https://whatwg.org/specs/web-apps/current-work/multipage/syntax.html#syntax-tag-omission)中查看新增了哪些可被忽略的标签。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Spending money, spending bytes&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;p&gt;Sic.&lt;/p&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre><pre><code>
&lt;!-- 推荐 --&gt;
&lt;!DOCTYPE html&gt;
&lt;title&gt;Saving money, saving bytes&lt;/title&gt;
&lt;p&gt;Qed.</code></pre>


#### type属性 ####
>在引用css或者javascript的时候，请省略type的声明，除非你使用的是其他的文件。在html5了，引用css或者js已经不需要为type指定默认值了。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;link rel=&quot;stylesheet&quot; href=&quot;//www.google.com/css/maia.css&quot;
  type=&quot;text/css&quot;&gt;
&lt;!-- 推荐 --&gt;
&lt;link rel=&quot;stylesheet&quot; href=&quot;//www.google.com/css/maia.css&quot;&gt;
&lt;!-- 不推荐 --&gt;
&lt;script src=&quot;//www.google.com/js/gweb/analytics/autotrack.js&quot;
  type=&quot;text/javascript&quot;&gt;&lt;/script&gt;
&lt;!-- 推荐 --&gt;
&lt;script src=&quot;//www.google.com/js/gweb/analytics/autotrack.js&quot;&gt;&lt;/script&gt;</code></pre>

## HTML格式规则 ##
#### 通用格式 ####
>对于块级元素、列表或者表格，你应该新起一行来书写它们。对于这些元素的子元素，应该采用缩进的写法。如果li元素内还包含子元素的话，是可以接受把他们都写在同一行。
><pre><code>&lt;blockquote&gt;
  &lt;p&gt;&lt;em&gt;Space&lt;/em&gt;, the final frontier.&lt;/p&gt;
&lt;/blockquote&gt;</code></pre>
><pre><code>&lt;ul&gt;
  &lt;li&gt;Moe
  &lt;li&gt;Larry
  &lt;li&gt;Curly
&lt;/ul&gt;</code></pre>
><pre><code>&lt;table&gt;
  &lt;thead&gt;
    &lt;tr&gt;
      &lt;th scope=&quot;col&quot;&gt;Income
      &lt;th scope=&quot;col&quot;&gt;Taxes
  &lt;tbody&gt;
    &lt;tr&gt;
      &lt;td&gt;$ 5.00
      &lt;td&gt;$ 4.50
&lt;/table&gt;</code></pre>

#### html中的引号 ####
>在html中，如果属性需要引用值得时候，应该采用双引号，而不是单引号。
><pre><code>&lt;!-- 不推荐 --&gt;
&lt;a class=&#x27;maia-button maia-button-secondary&#x27;&gt;Sign in&lt;/a&gt;
&lt;!-- 推荐 --&gt;
&lt;a class=&quot;maia-button maia-button-secondary&quot;&gt;Sign in&lt;/a&gt;</code></pre>

## css样式规则 ##
#### css的有效性 ####
>尽量使css代码是有效的，删除掉那些无效的css代码，尽管你觉得无效的css不会造成什么影响。除非是一些特殊的语法。 如果有必要，使用[W3C CSS validator](https://jigsaw.w3.org/css-validator/)来测试你的css代码。

#### id和class的命名 ####
>在id或者class命名的时候请尽量使其保持语义，能够反映出所属元素的功能。不要使用一些神秘或者随机的字符来命名，尽量不要使用拼音来命名。在兄弟元素或者功能相似的元素上，彼此的命名应该是有联系的。如果能够培养出固定的命名风格的话会让代码的语义更加良好。
>
>`#gallery {}`
>`#login {}`

>`.video {}`
>`.aux {}`
>`.alt {}`

#### id和class名称样式 ####
>id和class的名称应该尽可能的简短，并有利于阅读者理解。
>
>`#nav {}`
>
>`.author {}`

#### 选择器 ####
>如果可以的话尽可能的直接选择元素，而不是通过父级元素来查找，这样会造成性能的问题
>
>`/* 不推荐 */ul#example {}  div.error {}`
>
>`/* 推荐 */#example {}  .error {}`

#### 简写属性 ####
>尽可能的简写属性，减少代码量，为阅读带来便利。
><pre><code>/* 不推荐 */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;</code></pre><pre><code>
/* 推荐 */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;</code></pre>

#### 省略0后面的单位 ####
>在写属性值的时候，请省略0后面的单位：
>`margin: 0;
padding: 0;`

#### 第一位0省略 ####
>在写属性值时，如果写小数第一位是0，请省略它：`font-size: .8em;`

#### 十六进制写法 ####
>表达颜色值等其他情况，尽量写3位数的十六进制，更加精简：`color: #ebc;`。而不是6位数。

#### 命名前缀 ####
>在大型项目开发时（事实上小型项目也应该这样做），各个元素应该加上规范的前缀,用破折号链接它们，当作命名空间的作用，在团队合作之间减少冲突：

>`.adw-help {} /* AdWords */`
>
>`#maia-note {} /* Maia */`

#### 命名分隔符 ####
>在命名时，如果有两个单词以上，请不要直接将这些单词写在一起，影响可读性，应该使用`-`来链接：
>`.ads-sample {}`


#### hacks ####
>我们在处理一些滤镜或者其他在各个浏览器之间表现不一样的属性时，hack是我们常用的。但是应该尽量减少hack的使用，这是一种无奈之举。过多的hack让项目显得非常臃肿。

## CSS格式规则 ##

#### 书写顺序 ####
>在书写css属性时，我们应该养成固定的属性顺序。以便保持代码的统一性，比如-moz在-webkit之前。
><pre><code>background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;</code></pre>

#### 块内容的缩进 ####
>缩进所有的块内容，这样可以提高代码的层次感：
><pre><code>@media screen, projection {
	  html {
	    background: #fff;
	    color: #444;
	  }
}</code></pre>

#### 分号停止声明 ####
>在css声明时，每次都要以分号来结束声明，即使不写分号也没有什么影响：
><pre><code>/* 不推荐 */
.test {
  display: block;
  height: 100px
}
/* 推荐 */
.test {
  display: block;
  height: 100px;
}</code></pre>

#### 停止属性名称 ####
>在书写属性名称的时候，冒号后面应该跟一个空格，然后在书写属性值：
><pre><code>/* 不推荐 */
h3 {
  font-weight:bold;
}
/* 推荐 */
h3 {
  font-weight: bold;
}</code></pre>


#### 块的分离 ####
>各个块之间应该用空行分离开，并且在写完选择器之后追加一个空格再来继续写花括号
><pre><code>/* 推荐 */
.video {
    margin-top: 1em;
}</code></pre>

#### 选择器的分离 ####
>如果有多个选择器，那么应该使用逗号来分离它们：
><pre><code>/* 不推荐 */
a:focus, a:active {
  position: relative; top: 1px;
}
/* 推荐 */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}</code></pre>


#### 规则的分离 ####
>每个规则都应该新起一行来书写：
><pre><code>html {
  background: #fff;
}
</code></pre><pre><code>
body {
  margin: auto;
  width: 50%;
}</code></pre>


#### css引号 ####
>css应用值得时候应该使用单引号，而不是双引号：
><pre><code>/* 不推荐 */
@import url("//www.google.com/css/maia.css");
html {
  font-family: "open sans", arial, sans-serif;
}
/* 推荐 */
@import url(//www.google.com/css/maia.css);
html {
  font-family: 'open sans', arial, sans-serif;
}</code></pre>

## CSS规则元 ##
#### 注释 ####
>在每段css的头部应该有注释，来标记该段服务于什么内容：
><pre><code>/* Header */
.adw-header {}
/* Footer */
.adw-footer {}
/* Gallery */
.adw-gallery {}</code></pre>

## 结束 ##