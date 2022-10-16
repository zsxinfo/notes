# JavaScript DOM 编程艺术

## 上一版译者序

JS春天要来了，why？

DOM：Document Object Model 文档对象模型

Ajax技术以DOM和JS为基本要素

## 序

拓展三个新领域：
- html5
- Ajax
- js库 尤其是 jQuery

## 前言

写给设计师的。

真正目的：理解DOM脚本编程技术背后的 思路和原则。

## 第一章 JS简史

本书第一版 2006 第二版 2011

### 1.1 JS起源

Netscape和Sun公司合作开发。

JS1.0 1995 Netscape Navigator2 browser

ECMA：欧洲计算机制造商协会

ECMAScript

JS相对简单，需要通过Web浏览器去完成一些操作。

### 1.2 DOM

什么是DOM？

一套对文档的内容进行抽象和概念化的方法。

### 1.3　浏览器战争

Netscape　Navigator 4 发布于1997.6
IE4 发布于1997.10

这两种浏览器都对它们的早期版本进行许多改进，大幅拓展了DOM，使JS能完成的功能大大增加。同时DHTML也开始接触到。

#### 1.3.1 DHTML

DHTML：Dynamic HTML=html+css+js

NN4和IE4使用的是两种不兼容的DOM。

#### 1.3.2 浏览器之间的冲突

NN4: layer 层

document.layers['myelement']

IE4

document.all['myelement']

一种DOM脚本必须编写两次，而且还要写代码探查运行在哪种浏览器。

### 1.4 制定标准

W3C 1998.10 DOM level 1

var xpos = document.getElementById('myelement').style.left

标准化DOM可以让任何一种程序设计语言对使用任何一种标记语言编写出来的任何一份文档进行操控。

#### 1.4.1 浏览器以外的考虑

DOM是一种API（应用编程接口）。

类似于 莫尔斯码 国际时区 化学元素周期表

W3C对DOM的定义是：“一个与系统平台和编程语言无关的接口，程序和脚本可以通过这个接口动态地访问和修改文档的内容、结构和样式。”

#### 1.4.2 浏览器战争的结局

微软战胜了Netscape。

苹果 2003 Safari 基于 WebKit 从一开始坚定不移遵循DOM标准

### 1.5 小结

## 第二章 JS语法

### 2.1 准备工作

不需要特殊软件：文本编辑器+浏览器

### 2.2 语法

#### 2.2.1 语句

;

#### 2.2.2 注释

//

/* */

<!--    --> html 注释

#### 2.2.3 变量

JS不需要declaration

变量名区分大小写

变量名不允许空格和标点符号，除了$

#### 2.2.4 数据类型

类型声明 typing

强类型 strongly typed

弱类型 weakly typed

JS中最重要的几种数据类型：

1. 字符串
2. 数值
3. 布尔 true false

#### 2.2.5 数组

标量 scalar
数组 array

var beatles = Array(4);

var beatles = Array();

填充populating:

beatles[0] = "John";

关联数组：坏习惯；

#### 2.2.6 对象

var lennon = Object();
lennon.name = "John";
lennon.year = 1940;

var lennon = { name:"Jhon", year:1940, living:false };

### 2.3 操作

### 2.4 条件语句

if () {
    ;
}

严格比较  === !==

### 2.5 循环语句

和java一样

### 2.6 函数

function multiply(num1, num2) {
    var total = num1 * num2;
    return total;
}

### 2.7 对象

属性property和方法method都用dot访问

user-defined object用户定义对象

#### 2.7.1 内建对象

拿来就用的对象：native object 内建对象

Array.length

current_day.getDay() 今天是星期几

#### 2.7.2 宿主对象

不是JS提供的，而是浏览器提供的：host object，宿主对象

包括：
- Form
- Image
- Element
- document对象：获取网页上的任何一个元素的信息

### 2.8 小结

下一章 document对象 

基于DOM的基本编程思路，演示如何使用它的一些功能非常强大的方法。

## 第三章 DOM

5个常用的DOM方法：
- getElementById
- getElementsByTagName
- getElementsByClassName
- getAttribute
- setAttribute

### 3.1 文档：DOM中的D

### 3.2 对象：DOM中的O

对象：
- 用户定义对象
- native object: Array Math Date
- host object: 浏览器提供

window对象：浏览器窗口本身，这个对象的属性和方法通常统称为BOM（浏览器对象模型），但是我觉得Window Object Model更为贴切。window.open window.blur模糊。

### 3.3 模型：DOM中的M

M: 模型、Map

节点树

### 3.4 节点

node：网络术语

#### 3.4.1 元素节点

#### 3.4.2 文本节点

#### 3.4.3 属性节点

### 3.5 获取和设置属性

#### 3.5.1 getAttribute

#### 3.5.2 setAttribute

细节：通过setAttribute修改后，在浏览器里view source看源代码时仍将是改变前的属性值。

“表里不一”的现象源自DOM的工作模式：先加载文档的静态内容，再动态刷新，动态刷新不影响文档的静态内容。

### 3.6 小结

其他属性和方法：
- nodeName
- nodeValue
- childNodes
- nextSibling
- parentNode

下一章 利用DOM方法创建一个基于JS的图片库

## 第四章 案例：js图片库

### 4.4 对这个函数进行拓展

#### 4.4.1 childNodes属性

#### 4.4.2 nodeType

- elment 1
- attribute 2
- text 3

#### 4.4.3 标记里增加一段描述

#### 4.4.5 nodeValue属性

#### 4.4.6 firstChild和lastChild

### 4.5 小结

- childNodes
- nodeType
- nodeValue
- firstChild
- lastChild

下一章介绍一些JS脚本编程方面的最佳实践

达成目标的过程与目标本身同样重要

## 第五章 最佳实践

- 平稳退化：确保网页在没有JS的情况下也能正常工作。
- 分离JS：把网页的结构和内容与jS脚本的动作行为分开
- 向后兼容性：确保老版本的浏览器不会因为你的JS脚本而死掉
- 性能考虑：确保脚本执行的性能最优

### 5.1 过去的错误

#### 5.1.1 Don't blame js

it's the way people use it.

#### 5.1.2 Flash的遭遇

没有不好的技术，只有没有用好的技术。

#### 5.1.3 质疑一切

网站对js的滥用

### 5.2 平稳退化

graceful degradation

不要用伪协议调用。
### 5.3 向CSS学习

class id 单独的文件 link

### 5.4 分离JS

### 5.5 向后兼容

#### 5.5.2 浏览器嗅探技术

browser snuffing

### 5.6 性能考虑

#### 尽量少访问DOM和尽量减少标记

#### 减少加载页面时发送的请求数量：合并和放置脚本

#### 压缩脚本：上线前删除注释。

Douglas Crockford 的 JSMin

Yahoo's YUI Compressor

Google's Closure Compiler

### 5.7 小结

平稳退化；分离js；向后兼容；性能考虑；

## 第六章 案例：图片库改进版

- 把事件处理函数移出文档
- 向后兼容
- 确保可访问

### 6.3 js和html是分离的吗？

<ul id = "imagegallery">...</ul>

#### 6.3.1 添加事件处理函数

if (!document.getElementsByTagName) return false;

if (!document.getElementsById) return false;


if (!document.getElementById("imagegallery")) return false;

原则：如果想用js给某个网页添加一些行为，就不应该让js代码对这个网页的结构有任何依赖。

structed programming：结构化程序设计。

函数应该只有一个入口和一个出口。

#### 6.3.2 共享 onload 事件

window.onload = prepareGallery;

addLoadEvent(prepareGallery);

### 6.4 不要做太多的假设

### 6.5 优化

### 6.6 键盘访问

### 6.7 结合js和CSS

### 6.8 DOM Core 和 HTML-DOM

区分
- DOM Core ：不仅仅html，而且支持其他标记语言，比如XML
- HTML-DOM ：在DOM Core以前就为人熟知

### 6.9 小结

本章：
- 尽量不依赖假设，引入各种测试检查
- 没有使用onkeypress事件处理函数
- 分离js

我认为，结构和行为的分离程度越大越好。

下一章：如何利用DOM提供的方法和属性去创建HTML元素，并插入HTML文档。

## 第七章 动态创建标记

- 传统技术：document.write 和 innerHTML
- 深入剖析DOM方法；
    - createElement
    - createTextNode
    - appendChild
    - insertBefore

### 7.1 一些传统方法

document.write 不够优雅

#### 7.1.2 innerHTML属性

至少不用在body部分插入script标签

正宗XHTML会忽略innerHTML

### 7.2 DOM方法

setAttribute并未改变文档的物理内容，如果用文本编辑器而不是浏览器去打开这个文档，我们看不到任何变化。

只有用浏览器打开文档时才能看到文档呈现效果的变化。这是因为浏览器实际显示的是那棵DOM节点树。在浏览器看来，DOM节点树才是文档。

#### 7.2.2 appendChild 方法

#### 7.2.3 createTextNode

#### 7.2.4 一个更复杂的组合

### 7.3 back to 图片库

### 7.4 Ajax

2005年，Adaptive Path公司的Jesse James Garrett发明了Ajax这个词。

Ajax：异步加载页面内容的技术。

只更新页面中的一小部分。

呈现出功能丰富、交互敏捷、类似桌面应用般的体验，就像你使用谷歌地图时的感觉一样。

Ajax也有适用范围。第一，它依赖js；第二，搜索引擎的爬虫程序也不会抓取到有关的内容。

#### 7.4.1 XMLHttpRequest 对象

Ajax技术的核心就是：XMLHttpRequest对象。

这个对象就是浏览器中的脚本（客户端）与服务器之间的中间人角色。以往的请求都由浏览器发出，而js通过这个对象可以自己发送请求，同时也自己处理响应。

有关xmlhttprequest的标准比较新，但是这个对象的理事会可谓久远。

IE5 ： ActiveX对象 实现 XMLHTTP对象

var request = new ActiveXObject("Msxml2.XMLHTTP.3.0");

其他浏览器：

var request = new XMLHttpRequest();

不同IE版本用的XMLHTTP对象也不同，要用对象检测技术。

XMLHttpRequest有很多方法，其中最有用 的是open方法。要访问的文件，请求类型，以及指定请求是否以异步方式发送和处理。

request.open("GET", "xx.txt", true);

request.onreadystatechange = function() {
    //
}

request.onreadystatechange = doSomething;

request.send(null);

request.readyState属性的值：
- 0表示未初始化
- 1表示正在加载
- 2表示加载完毕
- 3表示正在交互
- 4表示完成

request.responseText

request.responseXML : Content-Type头部中指定为"text/xml"的数据，其实是一个DocumentFragment对象。你可以使用各种DOM方法来处理这个对象。

#### 7.4.2 渐进增强与Ajax

#### 7.4.3 Hijax

事实：Ajax应用主要依赖于服务器端处理，而非客户端处理了。

### 7.5 小结

更详细的Ajax和异步请求：请看12章。

下一章：更多向文档添加标记的例子，学会动态创建一些很有用的信息块来增强你的文档。

// 2022 10 14

## 第八章 充实文档的内容

- 缩略语列表 函数
- 文档来源链接 函数
- 快捷键清单 函数

### 8.1 不应该做什么

### 8.2 把“不可见”变成“可见”

### 8.5 显示“文献来源链接表”

displayAbbreviation 缩略语

displayCitation 文献来源

<blockquote cite="http://www.w3.org">

### 8.6 显示“快捷键清单”

accesskey

### 8.7 检索和添加信息

记住原则：

js脚本只应该用来充实文档内容，要避免使用DOM技术来创建核心内容。

### 8.8 小结

下一章：运用DOM处理颜色、字体等样式信息。

## 第九章 CSS-DOM

- style属性
- 如何检索样式
- 如何改变样式

### 9.1 三个层次

三位一体的网页：
- 结构层 html
- 表示层 CSS
- 行为层 JS

### 9.2 style属性

style属性只返回内嵌样式


### 9.3 何时改用DOM脚本设置样式

CSS :hover 

DOM :onmouseover

### 9.4 className属性

不改变style属性，只改变className属性

更进一步的抽象：

styleElementSiblings("h1", "intro");

### 9.5 小结

CSS永远也无法跟DOM竞争的应用：JS脚本能定时重复执行一组操作。通过不断改变样式，我们就能实现CSS根本不可能实现的效果。

下一章：你将写一个能够随着时间的推移而不断刷新元素位置的函数。简单地说，你将用jS实现动画效果。

## 第十章 用js实现动画效果

### 10.1 动画基础知识

position：
- static 默认值：按标记先后顺序
- reletive 类似static 但可以应用float
- absolute 位置与标记无关，而是top left right bottom决定
- fixed 

setTimeout

parseInt

parseFloat

### 10.2 实用的动画

CSS: overflow

- visible
- hidden
- scroll
- auto

使用hidden

### 10.3 小结

动画

下一章：html5

## 第十一章 HTML5

### 11.1 html5简介

- structure
- presentation
- behavior

结构层新增标记元素：<section> <article> <header> <footer>

交互及媒体元素：<canvas> <audio> <video>

新JS API：Geolocation Storage Drap-and-Drop Socket 及 多线程

### 11.2 来自朋友的忠告

用 Modernizr

### 11.3 几个例子

#### 11.3.1 Canvas

以前浏览器可做：
- 显示静态图片
- GIF实现动画
- CSS+JS变化样式

但是仅此而已。

难上加难：与静态图片交互。

HTML5的<canvas>使这一切成为历史。通过它可以动态创建和操作图形图像。

canvas涉及的数字及定位的概念与
- Adobe Illustrator
- 等基于矢量的图形软件
- 或者基于矢量的编程语言没有太大的差别。

以前在浏览器中实现高级的图片交互，只能依靠flash或者silverlight插件，但是今天有了canvas就可以在浏览器窗口绘制任何对象、任何像素了。

#### 11.3.2 音视频

容器：
- mp4: QuickTime MPEG4打包
- m4v: MPEG4
- avi: Audio Video Interleave 音视频交错
- flv: Flash Video
- mkv: ?

编解码器：
- H.264
- Theora
- VP8
- H.265

音频编解码器：
- mp3: MPEG-1 Audio Layer 3
- aac: Advanced Audio Coding
- ogg: Ogg Vorbis

H.264 编解码需要付费，但是传播不需要交钱

推荐书：

女博士 Silvia Pfeiffer

《The Definitive Guide to HTML5 Video》 2011

#### 11.3.3 表单

### 11.4 HTML5还有其他特性吗？

### 11.5 小结

- canvas
- audio video
- 表单 forms

## 第十二章 综合示例

本章：从头开始做一个网站，然后用js来为这个网站增加交互功能。

### 12.1 项目简介

为一个乐队涉及一个网站。

酷。交互。残疾友好，搜索引擎友好。

文件夹
- images
- styles: CSS files
- scripts: js files

页面：
- Home
- About
- Photos
- Live
- Contact

### 12.5 JS

### 12.6 小结

希望本书能让你对js和DOM产生初恋一般的美好感觉。

Web的无所不在是它的魅力。保证任何人都能无障碍地使用它 ，是一个最基本的原则。

## 附录：JS库

### A.1 选择合适的库

- 它具备你需要的所有功能吗？功能太少或不符合需求，不用。
- 它的功能是否比你想要的还多？太多了不好
- 它是模块化的吗？减少体积。
- 他的支持情况怎么样？bug有没有人修。
- 它有文档吗？没有文档看不懂，没前途。
- 它的许可合适吗？许可协议

有代表性的库：
- jQuery: 快速简洁，简化html文档搜索、事件处理、动画以及Ajax交互，快速web开发。强大的选择方法、连缀语法以及简化的Ajax和事件方法，使你的代码简洁且容易理解。
- Prototype：旨在简化动态web应用开发的框架。
- YUI：yahoo。简单DOM操作到高级效果，全功能的应用程序部件。
- Dojo Toolkit: 节省时间，性能优异。
- MooTools：小巧模块化面向对象的js框架。精巧、文档完备、前后一致的API，可以编写出强大、灵活而又能跨浏览器的代码。Moo.fx效果库令人叫绝。网页动画。

内容分发网络：CDN：content Delevery Network

### A.2 语法

选择函数：$()函数

jQuery each方法

### A.3 选择元素

通过CSS选择器选择：$('#elementid')

表单：
- :input
- :text
- :password
- :radio
- :checkbox
- :submit
- :image
- :reset
- :button

### A.4 操作DOM元素

操作DOM的能力可以体现一个库的水平

### A.5 处理事件

### A.6 Ajax

Ajax应用爆发后，js库也流行起来。

Prototype库（Ruby On Rails）就因为Ajax对象流行的。

### A.7 动画和效果

### A.8 小结

介绍了一些库，不可能面面俱到。

// 2022 10 16

## 作者

Jeremy Keith

Jeffrey Sambells























