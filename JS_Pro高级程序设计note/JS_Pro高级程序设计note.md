# JS高级程序设计

Matt Frisbie

译：李松峰

ECMAScript2019

12-17 js最辉煌的七年

JS红宝书 第三版 2012出版

# 序

by Zach Tratar

互联网革命是js造就的。

Brendan Eich 只用了10天就写出了jS第一版，所以不完美。但是无所不在这方面，js很接近完美。目前唯一一个可以随意部署的语言：服务器 桌面浏览器 手机浏览器 原生移动app。

Ajax 因为jQuery火了而变得更加流行，打开了通向新世界的大门。直到有一天遇到了发展瓶颈。

但突然间，强大的框架诞生了。前端模型、数据绑定、路由管理、反应式视图，全部爆发出来。

# 前言

全面深入地介绍了js开发者必须掌握的前端开发技术。

从起源开始，讲到最新的技术。重点讲ECMAScript和DOM标准。

在此基础上，揭示js基本概念，包括
- 类
- 期约
- 迭代器
- 代理

以及
- 客户端检测
- 事件
- 动画
- 表单
- 错误处理
- JSON

最后介绍近几年涌现的最新和最重要的规范
- Fetch API
- 模块
- 工作者线程
- 服务线程
- 大量新API

# 第一章 什么是js

1995：诞生：

代替Perl等服务端语言处理输入验证。

简单：学会只要几分钟

复杂：掌握要很多年

学号用好JS：理解本质、历史及局限性。

## 1.1 简短历史回顾

NN2浏览器 Mocha-LiveScript（LiveWire）-JS

1996.8 IE 微软进入web浏览器领域

1997 Ecma TC39

ECMA-262

## 1.2 JS实现

- 核心 ECMAScript
- 文档对象模型 DOM
- 浏览器对象模型 BOM

### 1.2.1 ECMAScript

宿主环境 host environment

定义了什么？
- 语法
- 类型
- 语句
- 关键字
- 保留字
- 操作符
- 全局对象

ECMA3

ECMA4难产 

ECMA3.1->ECMA5 2009

ECMA6 ES6 ES2015 2015.6
: 类 模块 迭代器 生成器 箭头函数 期约 反射 代理 新的数据类型

ECMA7 ES7 ES2016 2016.6
：修订 array.prototype.includes 指数操作符

ECMA8 ES8 ES2017 2017.6
：异步函数async/await SharedArrayBuffer AtomicsAPI ...

ECMA9 ES9 ES2018 2018.6
:异步迭代、剩余和拓展属性、一组 新的正则表达式特性...

ECMA10 ES10 ES2019 2019.6
:...

### 1.2.2 DOM

Document Object Model

文档对象模型 DOM 是一个API应用编程接口

DOM Level 1 1998.10成为W3C推荐标准。
- DOM Core
- DOM HTML

DOM Core提供了一种“映射XML文档，从而方便访问和操作文档任意部分”的方式。

DOM HTML拓展了DOM Core，并增加了特定于HTML的对象和方法。

DOM Level 2目标更宽泛。是DOM l1的拓展。增加了对一下内容的支持：
- 鼠标和用户界面事件
- 范围
- 遍历（迭代DOM节点的方法）
- CSS（通过对象接口）

另外，DOM Core拓展包含对XML命名空间的支持。

DOM Level 2新增以下模块：
- DOM视图：描述追踪文档不同视图的接口。
- DOM事件：描述事件及事件处理的接口
- DOM样式：描述处理元素CSS样式的接口。
- DOM遍历和范围：描述遍历和操作DOM树的接口

DOM level 3 进一步拓展DOM

DOM4

注：DOM0可以看作 IE4 NN4支持的DHTML。

### 1.2.3 BOM

浏览器对象模型 BOM API
- 弹出新窗口
- 移动、缩放和关闭窗口
- navigator对象：关于浏览器的详尽信息
- location对象：浏览器加载页面的详尽信息
- screen对象：关于用户屏幕分辨率的详尽信息
- performance对象：浏览器内存占用、导航行为和时间统计的详尽信息；
- 对cookie的支持
- 其他自定义对象：XMLHttpRequest

## 1.3 JS版本


# 第二章 HTML中的js

# 第三章 语言基础

ES6

## 3.1 语法

## 3.4 数据类型

- undefined
- boolean
- string
- number
- object
- function
- symbol

### 3.4.3 Null类型

// 2022 10 17

# 第四章 变量、作用域与内存
























