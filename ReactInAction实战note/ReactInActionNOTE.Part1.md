
# Part 1. Meet React

In Part 1, u'll start with the basics of React and learn them from the ground up. 

Because the tooling involved in building robust JavaScript UI app can be incredibly complex, we'll avoid getting bogged down in tools and focus on learning the ins and outs of the React API.

ins and outs: 前前后后；内情；迂回曲折；错综复杂事物的因果

be bogged down 陷入；被困住

ch1:
- components
- virtual DOM
- tradeoffs of React

ch2:
- whirlwind tour through React's APIs 旋风
- build a simple comment-box component to get your hands dirty with React.

## Chapter 1. Meet React

skeptical: 怀疑的

React is popular for good reason: it has a lot to offer and can reinvigorate 使再振作，再复兴(UI), renew(UI), or even transform how you think about and build user interfaces.

### 1.1 MEET REACT

helps you build UI in
- declarative way
- component-driven way

There was a time when React's approach was novel 新奇 异常 , but other tech has since been influenced by React's component-driven, declarative approach.

React continues to maintain a spirit of rethinking esstablished best practices, with the main goal being providing developers with an experssive 富于表现的 mental model and a performant 性能好的 运作良好的 technology to build UI app.

What makes React's mental model powerful? It draws on deep areas of CS and software engineering techniques.

Components often correspond to aspects of the UI, like
- datepickers,
- headers,
- navbars,
- and others

but they can also take responsibility for things like 
- client-side routing,
- styling,
- and others

an overview of the major ingredients 组成部分 that go into React application. Let's look at each part briefly:

- **Components** -- encapsulated 封装 units of functionality that are the primary unit in React. They utilize data(properties and state) to render ur UI as output. Certain types of components also provide a set of lifcycle methods that u can hook into. The *rendering process* (outputing and updating a UI based on ur data) is predictable in React, and ur components can hook into it using React's APIs.
- **React Libraries** -- React uses a set of core libs. The core React lib work with the **react-dom** and **react-native** libs and is focused on component specification and definition. It allows u to build a tree of components that a renderer for the browser or another platform can use. **react-dom** is one such renderer and is aimed at browser environments and server-side rendering. The React Native libs focus on native platforms and let u create React apps for iOS, Android, and other platforms.
- **Third-party libs** -- data modeling, HTTP calls, styling libs, and others.
- **Runing a React app** -- web, server; native; VR;



#### 1.1.1 Who this book is for

anyone interested in building UI.

U can learn how to build apps with React as long as U know the basics of JS and have some experience building web apps.

fundamentals of JS no cover:
- prototypal inheritance 原型继承
- ES2015+ code
- type coercion 类型强制
- syntax
- keywords
- asynchronous coding patterns like async/await 异步编程

Warning: get comfortable with the basics of JS before learning React. It's a wonderfully expressive and flexible language. You'll love it!

note 2022 10 14

### 1.1.2 A note on tooling

Webpack, Babel 

Tooling can be a distraction when learning a new technology like React. 

U're already trying to get Ur head around A new set of concepts and paradigms 范例 -- why clutter 弄乱 that with learning complex tooling too? 

That's why ch2 focuses on learning "vanilla" React first before moving on to features like JSX and JavaScript language features that require build tools.

The only tooling you'll need to be familiar with is npm.

### 1.1.3 Who uses React?

vibrant community 有活力的社区

robust ecosystem 强健的社区

daunting 令人畏缩的

## 1.2 What does react not do?

### 1.2.1 Tradeofffs of react

React : just the view

misconstrue 误解

React is not just a templating system like Handlebars or Pug (nee Jade) or that it has to be part of an MVC (model-view-controller) architecture.

React is a *declarative*, *component-based* library for building UI that works on a variety of platforms: web, native, mobile, server, desktop, and even on VR.

First tradeoff: React is primarily concerned with the *view* aspects of UI. 主要关注UI的视图方面。

This means it's not built to do many of the jobs of a more comprehensive framework or lib. 

A quick comparison to sth like Angular might help drive this point home. In its most recent major release, Angular has much more in common with React than it previously did in terms of concepts and design, but in other ways it covers much more territory 领土版图 than React. Angular includes opinionated solutions for the following:

- HTTP calls
- Form building and validation
- Routing
- String and number formatting
- Internationalization
- Dependency injection 依赖注入
- Basic data modeling primitives
- Custom testing framework
- Service workers included by default (a worker-style approach to executing js)

People's reaction to these features coming with framework:
- "Wow, I don't have to deal with all those myself"
- "Wow, I don't get to choose how I do anything."

大而全：Angular, Ember: there's usually a well-defined way to do things. Routing, HTTP tasks(HTTP routines).

React dosen't come with:
- HTTP
- routing
- data modeling

Most teams want the flexibility of React coupled with the mental model and intuitive APIs that it brings.

a set of powerful primitives 强大的原始工具

de facto 实际上存在

Downside obvious: U'll need to either come up with or find Ur own solution for different areas of Ur application. 

让工程师团队对决定或创造正确工具负起责任。

There's also the incredibly broader js ecosystem to consider -- u'll be hard-pressed 高压力 to find nothing aimed at problem u're solving.

remiss 怠慢 不小心 疏忽 粗心

lock-in 占据

interoperable 能共同操作的 能共同使用的

Migrating app is an area where React can shine. It employs relatively few "magic" idioms.

forgo 没有也行 放弃

incurring 招致

tightly 紧紧地

Another tradeoff: serve UI needs of FB.

wheelhouse 舵手室

include:
- app that don't work with conventional UI paradigms 传统UI范例 of modern web apps
- app that have very specific performance needs(such as a high-speed stock ticker.)

Last tradeoffs: React's' implementation and design.

a simpler mental model at the cost of not being able to do absolutely everything how u'd like.

Not only do you lose some visiblity (due to api design) to the underlying system, u alse buy into the way that react does things.

disingenuous 不真诚的

## 1.3 THE Virtual DOM

posit 假定 设想 假设

a major theme in react is a drive to simplify otherwise complex tasks and abstract unnecessary complexity away from the developer.

performant 有效的 高效的 高性能的 while freeing u up

one way:
- declarative √ 声明
- imperative x 祈使

You get to declare how ur components should behave and look under different states, and React's internal machinery handles the complexity of managing updates, updating the UI to reflect changes, and so on.

One of the major pieces of tech driving this is the virtual DOM.

A *virtual DOM* is a data structure that mimics or mirrors the Document Object Model that exists in browsers. I say a virtual DOM because other frameworks such as Ember employ their own implementation of a similar technology. In general, a virtual DOM will serve as an intermediate layer between the app code and the browser dom. the virtual DOM allows the complexity of change detection and management to be hidden from the developer and moved to a specialized layer of abstraction.

### 1.3.1 The DOM

### 1.3.2 The virtual DOM

inferior 下等的 下级的

原生DOM并不是不好，只是直接和DOM对接有些痛点，特别是大型网站。通常来说，痛点与change detection有关。

When data changes, we want to update the UI to reflect that. Doing that in a way that's efficient and easy to think about can be difficult, so React aims to solve that problem.

When a DOM element is accessed, modified, or created, the browser is ofen performing a query across a structured tree to find a given element. That's just to access an elemnt, which is usually only the first part of an update. It may have to reperform layout, sizing, and other actions as part of a *mutation* -- all of which can tend to be computationally expensive. A virtual DOM won't get you around this, but it can help updates to the DOM be optimized to account for these constraints 约束.

sizeable 大 相当大

subpar 低于标准的 在平均水平以下的

Thus 因此 performance is another key consideration in React's design and implementation. Implementing a virtual DOM helps address this, but it should be noted that it's designed to be just "fast enough".

A robust API, simple mental mode, and other things like cross-browser compatibity end up being more important outcomes of React's virtual DOM than an extreme focus on performance. 

### 1.3.3 Updates and diffing 

virtual DOM : 3D gamingd

从服务器获取需要更新的部分，然后给引擎渲染更新，而不是更新全部东西。

DOM mutation 变化 done poorly can be expensive, so React tries to be efficient in its updates to ur UI and employs methods similar to 3D games.

React creates and maintains a virtual DOM in memory, and a renderer like React-DOM handles updating the browser DOM based on changes. React can perform intelligent updates and only work on parts that have chagned because it can use *heuristic diffing* 启发式diffing to calculate which parts of the in-memory DOM require changes to the DOM. Theoretically, this is much more streamlined 流线型 经过简化以改善效率的 and elegant than "dirty checking" or other more brute-force approaches, but a major practical implication is that developers have less complicated state tracking to reason about.

diff and patch
- diff: what changed?
- patch: update only what changed.

### 1.3.4 Virtual DOM: Need for speed ?

snappy 迅速的 敏捷的

There's more to the virtual DOM than speed. 虚拟DOM不仅仅只是速度。

It's performant by design and generally results in snappy, speedy apps that are fast enouth for modern web app needs.

Performance is a key feature of React, but it's secondary to simplicity. 跟简化相比，性能不是最重要的。

The virtual DOM is part of what enables u to defer 推迟 thinking about complicated state logic and focus on other ,more important parts of ur app. Together, speed and simplicity mean happier users and happier developers -- a win-win.

extensively 广泛的 广大的

## 1.4 Components: the fundamental unit of react

Thinking in terms of components is essential for grasping 抓牢 抓紧 理解 领会 not only how React was meant to work but also how u can best use it in your projects.

### 1.4.1 Components in general

### 1.4.2 Components in React: Encapsulated and reusable 封装 重复利用

and composable 可组合的

spaghetti 意大利面条

constituent 选民 成分 组成元素

self-contained 自给自足的

Boundaries between components mean that functionallity and organization can be well-defined, whereas 然而 self-contained components mean they can be reused and moved around more easily.

Components in React are meant to work togetehre. This means u can *compose* together components to form new *composite* components 混合而成的components. Component composition is one of the most powerful aspects of React. U can create a component once and make it available to the rest of ur application for reuse.

A final aspect of React components is *lifecycle methods*. These are predictalbe, well-defined methods u can use as ur component moves through different parts of its lifecycle (mounting装备 装配, updating, unmounting, and so on.) We'll spend a lot of time on these methods in future chapters.

## 1.5 React for teams

hype 天花乱坠的广告宣传

fanatical 狂热的

There are many things that react doesn't do. but for the things it does do, it does extremely well.

What makes react great for large teams?

1. simplicity. simplicity != ease 安乐.

easy solutions are often dirty and quick, and worst of all, they can incur tech debt.

Truly simple tech is flexible and robust.

Simple tech is easier to understand and work with beacuse the difficult work of streamlining the removing what's not neccesary has been done. React has made simple easy, providing an effective solution without introducing harmful "black magic" or an opaque 不透明的 API.

All this is great for indivisual, but the effect is amplified 放大 across larger teams and orgs. 

2. React is a fairly lightweight lib in terms of respionsiblity and functionality.

interoperability 协同工作的能力 互用性

总的来说：
- simplicity
- un-opinionated nature
- performance

## 1.6 Summary

- Individual developer -- Once u learn react, ur app can be easier to rapidly build out. they will tend to be easier to work on for larger teams, and sophisticated features can be easier to implement and maintain.
- Engineering manager -- initial cost as they learn react, but eventually they will be able to easily and quickly develop complex apps.
- CTO or CEO -- investment with risks. gain in productivity and reduced mental burdens often outweight time sunk into ramping up.

// 2022 1018

# Chapter 2. \<Hello World />: our first component











