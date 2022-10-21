# Part2. Components and data in React

a handful of 少量

thoroughly 彻底地

ch3 : how data flows through a react app

ch4 : lifecycle methods in react; Understand React component API; start building a project that you will focus on for the rest of the book: a social networking app.

ch5,6 : look at forms in React;

ch7,8: routing; integrate Firebase so user can log into;

ch9 : testing : Jest Enzyme

wrap up 完成 结束 围好围巾 掩饰

# ch3. Data and data flow in React

cover:
- Mutable and immutable state
- Stateful and stateless components
- Component communication
- one-way data flow

## 3.1 State

cover:
- State
- How React handles state
- How data flows through components

Modern web app are usually built as data-first apps. Granted 诚然, there are many static sites (my blog ifelse.io), but even these are updated over time and generally considered to be in a different category form modern web apps. Most web apps that people use on a regular basis are highly dynamic and filled with data that changes over time.

### 3.1.1 What is state?

Definition:

All the infomation a program has access to at a given instant in time.

in other words, it's a snapshot of what you know about a program at an instant.

explicitly 明白地 明确地

JS employs what are called *run to completion* semantics, meaning that programs will be executed from top to bottom, in the order that you think they would be.

intersection 交叉点

### 3.1.2 mutable and immutable state

Redux : ch10 ch11 you'll emulate 效法 immutable DS

ephemeral 短暂的
persistent 持续的

## 3.2 STATE in React

props and state are 2 main ways that react compnents deal with data and communicate with each other.

### 3.2.1 Mutable state in React: Componnet state

From here on out , when I refer to staet I'm talking about the React API, not the general concept. 

Components that inherit from React.Componnet class will get access to this API.

Listing 3.2 Using setState to modify component state

call the *setState* method with an object as a prameter. 

Usually u want to use setState sparingly 节俭地 爱惜地 保守地 谨慎地. There are patterns that enjoy significant popularity in the React community that allow you to rarely use component state at all (including Redux, Mobx, Flux...), and these are great to explore as options for ur app -- in fact, we'll look at Redux in ch10 and ch11. Although it's better to use a stateless functional component, or rely on a pattern like Redux, using the setState API isn't a bad practice by itself -- it's still the main API in React for changing data in a component.

``` 
setState (
    updater,
    [callback]
) -> void
```

updater:
```
(prevState, props) => stateChange
```

key diffs from react 16: 

it could imply that setState was synchronous in nature, whereas what happens is that react will schedule a change to state.

The callback format better communicates thsi idea and is generally more consistent with react's overall declarative asynchronous 异步 paradigms: u allow the system to schedule updates where order but not time are guarnteed.

If u need to make an update to state that depends on the current state or props, u can access those through the *prevState* and *props* arguments. That's often useful when u want to do sth like toggle 开关 a boolean and need to know the exact last value before performing an update.

Lets focus on the mechanics of setState a little more. Using the objecet returned from ur updater function, it performs a shallow merge into current state. This means u can yield an object and react will merge top-level properties on the object into state.

immutable.js recommend

setState is a straightforward API to use;

### 3.2.2 Immutable state in React : Props

js: Object.freeze

props are data that gets passed to react components, either from a parent or from the defaultProps static method on the component itself. Whereas component state is localized to a single component, props are usually passed from a parent component. If you re thinking "can i use state in a parent componnet to pass props to a child component?" u are onto something. 

one-way down : from parent to child 

parent's state can be child's props: thus change parent's state can chagne child's props.

### 3.2.3 working with props: propTypes and default props

proptypes and default props: available to help you.

PropTypes provides a typechecking func in which u can specify what sort of props your component will expect to receive when used. 

https://github.com/faceboook/prop-types

Listing 3.4 Immutable props in React components

### 3.2.4 stateless functional components

stateless component

functional component

no lifecycle methods, no component state and potentially less memory.

Stateless functional components are functional because they can be written as named functions or anonymous function expressions assigned to a variable. They only take props and, because they return the same output based on a given input, are essentially considered pure. This makes them fast, as React will potentially be able to make optimizations by avoiding unnecessary lifecycle checks or memory allocations. 

stateles  functional components can be powerful, especially when used in combination with a parent component that has a backing instance. Rather than having to set state across multiple components, you can create a single stateful parent componetn and use lightweight child components for the rest. In ch10 adn 11, we'll look at using Redux to take this pattern to  a whole new level. In React apps that use Redux, you usually end up creating fewer stateful components (although there are still cases where this makes sense) and isntead centralize state in a single location (the store).

#### using state in one componnet to modify props in another

Listing 

https://codesandbox.io/s/38zq71q75

## 3.3 Component communication

is-a, has-a relationships between components.

If u want components to communicate with each other, u pass props, and when u pass props, u're doing 2 simple things:
- Accessing data in the parent(either state or props)
- Passing that data to a child component

Listing 3.6

https://codesandbox.io/s/pm18mlz8jm

## 3.4 One-way data flow

the term "two-way data binding"

binding between app UI and other data.

manifest 出现

projection

UI is the data projected into a view.

data flow : how does data move through different parts of ur app? Essentially u're asking, "what can update what, from where, and how?" 

It's important to understand how the tools u are using shape manipulate and move data around if u want use them well. 

In react, data flow in one direction. hierarchy established.

can't modify the data in parent. but can pass data back up the hierarchy via callbacks.

When a parent receives a callback from a child component, it can change its data and send the changed data back down to the child components. Even in this scenario with callbacks, data still flows downwards in aggregate and remains determined by the parent passing the data down.

Unidirectional flow is especially helpful in buiding UIs because it tends to make it easier to think about the way data moves through an app. Thanks to the hierarchy of components and the way props and state are localized to components, it's generally easier to predict how data moves thourgh aan application.

It might sound nice in some ways to eschew 避开 远离 this hierarchy and have the freedom to modify whatever you want from any part of your app, but in practice that tends to lead to app that are hard to think about and can result in difficult debugging situation. 

Later chapters will explore architectural patterns like Flux and Redux that allows u to maintain a unidirectional 单向的 data flow paradigm while coordinating actions that can occur across components or across ur app.

## 3.5 SUMMARY

- State is the infomation available to a program at a given moment in time.
- Immutable state doesn't chagne, whereas mutable state does change.
- Persitent, immutable data structures don't chagne -- they only record their changes and make copies of themselves.
- Ephemeral, mutable data structures are wiped out when they are updated.
- React uses both mutable(local component state) and pseudo-immutable data(props)
- Props are pseudo-immutable and should not be modified once set.
- Component state is tracked by a backing isntance and can be modified with setState
- setState performs a shallow 浅的 merge of data and updates ur component's state, preserving any top-level properties that aren't overwritten.
- Data flows one way in React, from p to child. children can yield 生产 back via a callback, but they can't directly modify the parent's state, and a parent cna't directly modify a child's state. Component interaction is done via props isntead.

In ch4, we'll build on ur knowledge of state in React and look at how to use lifecycle methods to hook into React's render and update process. We'll also start to explore change detection in React and you'll start to build out the social app using ur newly learned react skills.

# Ch4. Rendering and lifecycle methods in React

covers:
- set up app repository
- rendering process
- lifecycle methods
- updating react components
- creating a newsfeed using react

lifecycle methods and rending process

## 4.1 Getting set up with repo

by the end of the book, Letter Social will be using server-side rendering, Redux and React.

- creating  posts that have text
- adding location to posts with Mapbox
- Liking and commenting on posts
- providing OAuth authentication via GitHub and Firebase
- Displaying posts in a newsfeed
- Using basic pagination 分页

if you would like to get a sense of the code and you like JSDoc-style documentation, the docs will be a good place to go. The README for the repo also lists a number of helpful resources. As always, feel free to reach out to me if you have questions.

https://docs.react.sh

### 4.1.1 getting the source code

source code:

https://github.com/react-in-action/letters-social

All the modules you'll need for the entire book should be included in package.json in the app source. To install, run "npm install" in source code directory.

### 4.1.2 which version of node should i use?

NVM: install copies of node locally and switch between them

### 4.1.3 Node on tooling and CSS

tooling around js app can be a complex and fast-moving target. It's also a domain that deserve its own treatment.

For these reasons, I won't be covering how to set up things like Webpack, Babel, or other tools. The app source code has a development and build process in place, and you re free to explore the configuration I've set up, but that's outside the scope of this book,, so I won't be covering it.

CSS is outside scope.

### 4.1.4 Deploying

the app is deployed to https://zeit.co (ZEIT is now Vercel). 

https://vercel.com 

build and runtime processes are straightforward, so you should find it relatively easy to deploy somewhere else.

### 4.1.5 The API server and database

To prevent u from having to run a database like MongoDB or PostgreSQL, we'll use a simulated REST API via the JSON-server library.

https://github.com/typicode/json-server

I've made some modifications to the default server (which you can see in the db folder of the repo) that help make the project a little bit easier. Rather than work with a database, you will get a lightweight database that works by reading and modifying a JSON file. To create sample data or reset your app data, you can run this command: 

```
npm run db:seed
```

That will overwrite the existing JSON database and replace it with new sample data.

a number of helpers to make it easier to make request to the API. see

src/shared/http.js

making use of the isomorphic-fetch library

https://github.com/matthew-andrews/isomorphic-fetch

because it mirrors the standard Fetch API available in browsers, but also runs on the server. I'll assume you have some experience with an HTTP library in the browser, but if not you can use the included helper files as a way to start learning about the Fetch API.

https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

### 4.1.6 Running the app

```
npm run dev
```

```
npm run 
```

## 4.2 The render process and lifecycle methods

key features of React, once you know them you will be better equipped to start building the letter social app.

- render process
- lifecycle methods

### 4.2.1 Introducing lifecycle method

Definition

Lifecycle methods are special methods attached to class-based React components that will be executed at specific points in a component's lifecycle. 

A lifecycle is a way of thinking about a component. 

A component with a lifecycle has a metaphorical "life" -- it has at least a beginning, middle, and end.

Main part of a life are:
- mounting 安装
- updating
- unmounting

hindrance 起妨碍作用的事物或人

### 4.2.2 Types of lifecycle methods

two main group:
- Will methods -- called right before sth happens
- Did methods -- called right after sth happens

four main parts of their lifecycle:
- Initialization
- Mounting -- being inserted to the DOM
- Updating 
- Unmounting -- being removed from the DOM

### 4.2.3 Initial and "will" methods

- defaultProps -- A static property that provides the default props for a component. Sets on *this.props* if that prop is not set by  the parent componnet, is accessed before any componnets are mounted, and can't rely on *this.props*. or *this.state.*. beccause defaultProps is a static property, it's accessed from the class, not instance.

- state(initial) -- The value of this property in the constructor will be the initial value set for the state of ur component. That's especially helpful when you need to provide placeholder content, set default values, or the like. It's similar to default props with the exception that the data is expected to be mutated and only available on components that inherit from React.Component.

### 4.2.4 Mounting components

A common mistake people make when learning react is putting things in render() that shouldn't be. You can't know exactly when React will call render() because it batches updates for performance reasons.

componentWillMount : the only chance to change state before mounted

componentDidMount : good place to do like update your component state with data coming back form a network request. Also good place to work wtih third-party libraries that depend on DOM, like jQuery or others.

If u execute handlers or other functions in other methods (like render()) , you will end up with unpredictable and unexpected results due to how React works. Render methods need to be *pure*(consistent based on a given input) and are usually called many times over the lifetime of a component.

### 4.2.5 Updating methods

- shouldComponentUpdate()
- componentWillUpdate()
- componentDidUpdate()

### 4.2.6 Unmounting methods

If your app is writen all with React a router (ch8, ch9) will remove components as you move between different pages. 

componentWillUnmount : cleanup

There's not componentDidUnmount

### 4.2.7 Catching errors

componentDidCatch()

try...catch

Table 4.1 summary of the methods covered so far.

## 4.3 Starting to create letters-social

use Webpack build process included with the repo, for reasons:

- able to write js in many files that are output in one or a small handful of files that have automatically resolved dependencies and import order.
- able to handle and process different types of files
- to utilize other build tools like Babel so you can write modern js that will run on older browsers
- to optimize js by removing dead code and minifying it

Webpack is an incredibly powerful tool used by many teams and companies. As stated earlier in the chapter, I won't cover how to use it.

``` 
import React, { Component } from 'react';
import { Render } from 'react-dom';

import App from './app';

import './shared/crash';
import './shared/service-worker';
import './shared/vendor';
import './styles/styles.scss';

render(<App />, document.getElementById('app'));
```

src/app.js : create the main App component

sketch out 素描

skeleton 骨架

flesh out 充实 具体化

keep adding functionality to the app as u explore different topics in React like testing, routing, and application architecture (using Redux).

Listing 4.8 Creating the App component (src/app.js)

Running "npm run dev" will do a few things for you:

- Start up the Webpack build process and development server
- Start the JSON-server API so you can respond to network requests
- Create a development server (useful for server-side rendering in ch12)
- Hot-reload your app when changes occur (so you don't have to refresh the app every time you save a file)
- Notify you of build errors (these should show up in the command line and the browser if and when they occur)

running app at http://localhost:3000

API server runing at http://localhost:3500


YOU need to fetch data from the API and then update component state with that data.

You'll also add an error boundary sothat if your component encounters an error you can show an error message instead of the entire app unmounting.

how to add the class methods to the App component

```
//...
    constructor(props) {
        //...
        this.getPosts = this.getPosts.bind(this);
    }
    componentDidMount() {
        this.getPosts();
    }
    componentDidCatch(err, info) {
        console.error(err);
        console.error(info);
        this.setState( () => ( {
            error: err;
        }));
    }
    getPosts() {
        API.fetchPosts(this.state.endpoint).then
        ( res => {
            return res
                .json()
                .then ( post => {
                    const links = parseLinkHeader(res.headers.get('link'));
                    this.setState( () => ( {
                        posts: orderBy(this.state.posts.concat(posts), 
                        'date', 'desc'),
                        endpoint: links.next.url
                    }));
                })
                .catch(err => {
                    this.setState(() => ({error: err}));
                });
        })
    }
    render() {
        //...
        <button className="block" onClick = {this.getPosts}>
            load more posts
        </button>   
        //...
    }
```

2 set up an error boundary for the app so you can handle errors

3 Fetch post using the included API module

4 The API module uses the Fetch API, so you need to unwrap 打开、展开 the JSON response

5 The letters-social API returns pagination 分页information in headers, so you can use the parse-link-header to pull the URL for the next page of posts out.

6 add new posts to state and ensure they're sorted correctly.

7 update the endpoint state

8 if there's an error , update component state

9 Now that you have it definedd, assign the getPosts method to the load more event handler.

next : post components

Listing 4.10 Creating the Post Component

next : iterate over the posts so they get displayed

Remenber that the way to display a dynamic list of components is to construct an array (either through Array.map or another mehtod) and use that in a JSX expression.

how to update the *render* method of the App component to iterate over posts.

Listing 4.11 Iterating over Post components (src/app.js)

```
<div>
    {this.state.posts.length && (
        <div className="posts">
            { this.state.posts.map(
                ( {id} ) => (
                    <Post id={id} key={id} user=(this.props.user) />
                )
            )}
        </div>
    )}
    <button>
</div>
```

next chapter: add post; add location to post

explore using refs -- a way to access underlying DOM elments from your React components

## 4.4 Summary

what we learned in this chapter:
- React components inherit from React.Component
- lifecycle methods : write only when you need them
- handling errors that occur in *constructor*, *render*, or lifecycleMethods::: use *componentDidCatch*.
- start building letter-social

next: create posts dynamically and even add locations to posts using Mapbox

// 2022 10 21

# ch5: Working with forms in React

cover:
- using forms in React
- controlled and uncontrolled form components in React
- Validating and sanitizing data in React

## 5.1 Creating post in letter-social
















