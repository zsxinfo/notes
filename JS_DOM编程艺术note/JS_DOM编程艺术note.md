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




















