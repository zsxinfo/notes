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

本章：
- 通过变量使用原始值与引用值
- 理解执行上下文
- 理解垃圾回收

本章会剖析错综复杂的变量。

## 4.1 原始值与引用值

原始值 primitive value : by value
- number
- string
- symbol
- boolean
- null
- undefined

引用值 reference value : by reference
- object
- function

注意：在很多语言中，String 是引用类型

### 4.1.1 动态属性

只有引用值可以动态添加后面可以使用的属性

如果用new 关键字，js会创建一个Object的实例，但行为类似原始值

### 4.1.2 复制值

Object在堆内存中，变量只是保存一个指向object 的指针。

### 4.1.3 传递参数 

传参

ECMASCript中，所有函数的参数都是按值传递的。

pass by value

js and java is always pass by value

### 4.1.4 确定类型

typeof 虽然对原始值很有用，但它对引用值的用处不大。

instanceof 它是什么类型的对象

console.log(person instanceof Array); //person是Array吗

## 4.2 执行上下文与作用域

每个上下文都有一个关联的**变量对象**variable object

这个上下文中定义的所有变量和函数都存在于这个对象上

全局上下文：window对象（ch12）

var : 全局

上下文栈：先进后出

作用域链 scope chain

活动对象 activation object

### 4.2.1 作用域链增强

- try/catch 的 catch
- with

### 4.2.2 变量声明

let const

Object.freeze();

freeze之后，赋值不会报错，但会静默失败

## 4.3 垃圾回收

### 4.3.1 标记清理

mark-and-sweep

### 4.3.2 引用计数

reference counting

### 4.3.3 性能

### 4.3.4 内存管理

如果数据不再必要，则设置为null，从而释放其引用，这也叫**解除引用**。

隐藏类

内存泄漏

## 4.4 小结

# 第五章 基本引用类型

- 理解对象
- 基本js数据类型
- 原始值与原始值的包装类型

引用类型 != 类

引用类型 也成为 对象定义

对象 被认为是 某个特定引用类型的**实例**

new 后面跟一个**构造函数** constructor

函数也是一种引用类型 ch10

## 5.1 Date

Date 参考了java早期版本中的 java.util.Date

UTC 1970.1.1 00:00 至今经过的毫秒数

可以表示+-285616年

Date.parse()
- "5/23/2019"
- "May 23, 2019"
- "Tue May 23 2019 00:00:00 GMT-0700"
- "2019-05-23T00:00:00" (兼容ES5)

Date.UTC()

月数 0 - 1月 1 - 2月
日 1---31
时 0-23

Date.UTC(2000, 0)

UTC默认用本地时间， parse默认用GMT

toLocalString() AMPM 无时区信息

toString() 带时区信息 24小时制

valueOf() 日期的毫秒表示

toDateString() 周几、年月日

toTimeString() 时分秒、时区

toLocaleDateString() 周几、年月日

toLocaleTimeString() 时分秒

toUTCString() 显示完整的UTC日期

表格： Date类型的剩下方法

## 5.2 RegExp

RegExp 类型 支持 正则表达式

正则表达式使用类似Perl的简洁语法来创建

let expression = /pattern/flags;

pattern 可以是任何正则表达式
- 字符类
- 限定符
- 分组
- 向前查找
- 反向引用

每个正则表达式可以带0个或多个flags（标记），用于控制正则表达式的行为：

- g 全局，查找全部，而不是找第一个
- i 不区分大小写 查找匹配时忽略pattern和字符串的大小写
- m 多行模式 查找到一行文本末尾时会继续查找
- y 粘附模式，表示只查找从lastIndex 开始及之后的字符串
- u Unicode模式，启用Unicode匹配
- s dotAll模式，表示元字符，匹配任何字符

let pattern1 = /at/g;

let pattern2 = /[bc]at/i  // 匹配第一个bat或者cat，忽略大小写

let pattern3 = /.at/gi  // 匹配所有以"at"结尾的三字符组合，忽略大小写

所有**元字符**必须转义，包括：

( [ { \ ^ $ | } ] ) ? * + .

let pattern4 = /\.at/gi //匹配所有'.at'，忽略大小写

let pattern 2 = new RegExp("[bc]at", "i");

### 5.2.1 RegExp实例属性

- global : g
- ignoreCase : i
- unicode : u
- sticky : y
- lastIndex : 0
- multiline : m
- dotAll : s
- source : 字面量字符串
- flags : 标记字符串

### 5.2.2 RegExp 实例方法

exec() 用于配合捕获组使用

test() 常用于if语句，比如测试用户输入是否有效

### 5.2.3 RegExp 构造函数属性

- input $_
- lastMatch $&
- lastParen $+
- leftContext &`
- rightContext $'

$1~$9 : 包含第1~9个捕获组的匹配项

注：RegExp构造函数的所有属性皆非标准

### 5.2.4 模式局限

缺少Perl语言中的一些高级特性

参考 regular-expressions.info 网站

- \A和\Z锚（分别匹配字符串的开始和末尾）
- 联合及交叉类
- 原子组
- x（忽略空格）匹配模式
- 条件式匹配
- 正则表达式注释

## 5.3 原始值包装类型

Boolean Number String 类似java？

### 5.3.1 Boolean

所有Object在布尔表达式中都会自动转换为true

let falseObject = new Boolean (false)

if (falseObject) // true 

这一点和java不一样

因此永远不要用这个类型

### 5.3.2 Number

let num = 10;

num.toString(16) // "a" 16进制

num.toString(2) // "1010" 2进制

num.toFixed(2) // "10.00" 保留两位小数的数值字符串

num.toExponential(1) // "1.0e+1" , 1表示结果中小数的位数

num.toPrecision() 根据情况返回最合理的输出结果

isInteger()

isSafeInteger()

### 5.3.3 String

charAt()

两种Unicode编码混合： UCS-2 UTF-16，对于可以采用16位编码的字符（U+0000~U+FFFF），这两种编码实际上是一样的。

推荐博文by Joel Spolsky：

<a href = "https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/"> The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets (No Excuses!) </a>

另一个有用的博文by Mathias Bynens

<a href = "https://mathiasbynens.be/notes/javascript-encoding">JavaScript's Internal Character Encoding: UCS-2 or UTF-16?</a>

charCodeAt()

length

fromCharCode()

codePointAt() 代替 charCodeAt()

fromCodePoint() 代替 fromCharCode()

#### normalize()

Normalization Form

4种规范化形式
- NFD
- NFC
- NFKD
- NFKC

#### 字符串操作方法

concat()

+

slice()

substr()

substring()

#### 字符串位置方法

indexOf()

lastIndexOf()

#### 字符串包含方法

startsWith()

endsWith()

includes()

#### trim()

删除前后空格

#### repeat()

复制+拼接

#### padStart() padEnd()

let s = "foo"

s.padStart(6) // "   foo"

s.padEnd(6) // "foo   "

s.padEnd(6, ".") // "foo..."

#### 字符串迭代与解构

@@iterator

```
let message = "abc"
let strIte - message[Symbol.iterator]();
strIte.next(); // {value: "a", done:false}
strIte.next(); // {value: "b", done:false}
```

for-of循环
```
for (const c of "abcde") {
    console.log(c);
}
```


有了这个迭代器后，字符串就可以通过结构操作符来结构了。比如，可以更方便地把字符串分割为字符数组：
```
let message = "abcde";

console.log([...message]); // ["a", "b", "c", "d", "e"]
```

#### 字符串大小写转换

toLowerCase()

toLocaleLowerCase()

toUpperCase()

toLocaleUpperCase()

#### 字符串模式匹配方法

match() 跟RegExp的exec() 相同。

search()

replace()

$n $nn $$ $& $' $` 

```
let text = "cat, bat, sat, fat";
result = text.replace(/(.at)/g, "word ($1)");
console.log(result); // word (cat), word (bat), word (sat), word (fat)
```

split()

````
colortext = "red,blue,green,yellow";
let colors3 = colortext.split(/[^,]+/);
// ["", ",", ",", ",", ""]
````

注意 [^,]表示匹配除了‘,’以外的任意字符（反义字符），+表示重复一次或更多次（限定字符）

为什么返回的数组前后包含两个空字符串？

这是因为正则表达式指定的分隔符出现在了字符串开头和末尾（"red" "yellow"）

#### localeCompare()

大写排小写前面 ，US

#### HTML方法

无人使用。

## 5.4 单例内置对象

### 5.4.1 Global

最特别的对象。全局都是Global的属性。

#### URL编码方法

encodeURI();

decodeURI();

encodeURIComponent();

decodeURIComponent();


#### eval()

不会被提升

#### Global对象属性

- undefined
- NaN
- Infinity
- Object
- Array
- Function
- Boolean
- String
- Number
- Date
- RegExp
- Symbol
- Error
- EvalError
- RangeError
- SyntaxError
- TypeError
- URIError

#### window 对象

ch12

let global = function() {
    return this;
} ();

### 5.4.2 Math

Math 更高效

#### 属性

- Math.E
- Math.LN10
- Math.LN2
- Math.LOG2E
- Math.LOG10E
- Math.PI
- Math.SQRT1_2
- Math.SQRT2

#### min() max()

#### 舍入方法

Math.ceil() 向上

Math.floor()

Math.round()

Math.fround() 返回数值最接近的单精度32位浮点值表示

#### random()

0,1范围内随机数 包含0不包含1

#### 其他方法

## 5.5 小结

js中的object称为引用值。

js中比较独特的一点是，函数实际上时Function类型的实例，也就是说函数也是对象。

// 2022 10 21

# 第六章 集合引用类型
















