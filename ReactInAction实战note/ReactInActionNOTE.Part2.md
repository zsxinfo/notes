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

### 5.1.1 Data requirements

Use some browser HTTTP libraries to send data to API server.

No cover: How to communicate with RESTful APIs from JavaScript.

推荐书 

JavaScript Application Design by Nicolas G. Bevacqua

define Post class

### 5.1.2 Component overview and hierarchy

Listing 5.2 creating a componnet skeleton (sr/componnets/post/create.js)

```
import React, { Componnet } from 'react';
import PropTypes from 'prop-types';

class CreatePost extends Component {
    static propTypes = {

    }
    constructor (props) {
        super(props);
    }
    render() {
        return (
            <div className="create-post">
                Create a post - coming soon
            </div>
        );
    }
}

export default CreatePost;
```

## 5.2 FORMS in React

### 5.2.1 start forms

forms are just more of what we've seen so far in React: components! You use components, state, and props to create forms.

Review:
- state and props
- custom class methods and lifecycle hooks
- listen for events like clicks, input changes
- Parent component (form elements) can provide callback methods as props to child components, making it possible for components to communicate with each other.

### 5.2.2 Form elements and events

Listing 5.3 Adding to your creaete Post component

```
import React, { Componnet } from 'react';
import PropTypes from 'prop-types';

class CreatePost extends Component {
    static propTypes = {

    }
    constructor (props) {
        super(props);
    }
    render() {
        return (
            <div className="create-post">
                <textarea
                    placeholder="What's on your mind?"
                />
                <button>Post</button>
            </div>
        );
    }
}

export default CreatePost;
```

two main event handlers: 
- onchange: access the new value of the form element using event.target.value
- onClick

Listing 5.4 adding to your createPost component

```
import React, { Componnet } from 'react';
import PropTypes from 'prop-types';

class CreatePost extends Component {
    static propTypes = {

    }
    constructor (props) {
        super(props);
        this.handleSubmit = this.handleSubmit.bind(this);
        this.handlePostChange = this.handlePostChange.bind(this);
    }
    handlePostChange(e) {
        console.log(e.target.value);
    }
    handleSubmit() {
        console.log("handling submisssion!");
    }
    render() {
        return (
            <div className="create-post">
                <textarea
                    value={this.state.content}
                    onChange={this.handlePostChange}
                    placeholder="What's on your mind?"
                />
                <button onClick={this.handleSubmit}>Post</button>
            </div>
        );
    }
}

export default CreatePost;
```

Table 5.1 properties and methods available on a synthetic event in React

synthetic event: React translates the browser event into sth you can work with in React component.

- bubbles
- cancelable
- currentTarget
- defaultPrevented
- evetnPhase
- isTrusted
- nativeEvent
- preventDefault()
- isDefaultPrevented()
- stopPropagation()
- isPropagationStopped()
- target
- timeStamp
- type

### 5.2.3 Updating state in forms

Listing 5.5 Updating component state using inputs

```
import React, { Componnet } from 'react';
import PropTypes from 'prop-types';

class CreatePost extends Component {
    static propTypes = {

    }
    constructor (props) {
        super(props);
        this.state = {
            content: '',
        };
        this.handleSubmit = this.handleSubmit.bind(this);
        this.handlePostChange = this.handlePostChange.bind(this);
    }
    handlePostChange(event) {
        const content = (event.target.value);
        this.setState( () => {
            return {
                content,
            };
        });
    }
    handleSubmit() {
        console.log(this.state);
    }
    render() {
        return (
            <div className="create-post">
                <textarea
                    value={this.state.content}
                    onChange={this.handlePostChange}
                    placeholder="What's on your mind?"
                />
                <button onClick={this.handleSubmit}>Post</button>
            </div>
        );
    }
}

export default CreatePost;
```

### 5.2.4 Controlled and uncontrolled components

listing 5.6 uncontrolled pattern

```
import React, { Componnet } from 'react';
import PropTypes from 'prop-types';

class CreatePost extends Component {
    static propTypes = {

    }
    constructor (props) {
        super(props);
        this.state = {
            content: '',
        };
        this.handleSubmit = this.handleSubmit.bind(this);
        this.handlePostChange = this.handlePostChange.bind(this);
    }
    handlePostChange(event) {
        const content = (event.target.value);
        this.setState( () => {
            return {
                content,
            };
        });
    }
    handleSubmit() {
        console.log(this.state);
    }
    render() {
        return (
            <div className="create-post">
                <textarea
                    // no set value
                    onChange={this.handlePostChange}
                    placeholder="What's on your mind?"
                />
                <button onClick={this.handleSubmit}>Post</button>
            </div>
        );
    }
}

export default CreatePost;
```

### 5.2.5 Form validation and sanitization

questions:
- what are the data requirements for the app?
- based on these constraints, how can you help your users provide meaningful data?
- are there ways you can eliminate inconsistencies in data that users provide?

listing 5.7 adding basic validation

```
import React, { Componnet } from 'react';
import PropTypes from 'prop-types';

class CreatePost extends Component {
    static propTypes = {

    }
    constructor (props) {
        super(props);
        this.state = {
            content: '',
            valid: false, // 1
        };
        this.handleSubmit = this.handleSubmit.bind(this);
        this.handlePostChange = this.handlePostChange.bind(this);
    }
    handlePostChange(event) {
        const content = (event.target.value);
        this.setState( () => {
            return {
                content,
                valid: content.length <= 280 // 2
            };
        });
    }
    handleSubmit() {
        if (!this.state.valid) {
            return;
        }
        const newPost = {   // 3
            content: this.state.content,
        };  
    }
    render() {
        return (
            <div className="create-post">
                <textarea
                    value={this.state.content}
                    onChange={this.handlePostChange}
                    placeholder="What's on your mind?"
                />
                <button onClick={this.handleSubmit}>Post</button>
            </div>
        );
    }
}

export default CreatePost;
```

Sanitization

js module : bad-words , from npm

Listing 5.8 Adding basic content sanitization

```
import React, { Componnet } from 'react';
import PropTypes from 'prop-types';

import Filter from 'bad-words'; // 1

const filter = new Filter();    // 2

class CreatePost extends Component {
    static propTypes = {

    }
    constructor (props) {
        super(props);
        this.state = {
            content: '',
            valid: false, // 1
        };
        this.handleSubmit = this.handleSubmit.bind(this);
        this.handlePostChange = this.handlePostChange.bind(this);
    }
    handlePostChange(event) {
        const content = filter.clean(event.target.value);   // 3
        this.setState( () => {
            return {
                content,
                valid: content.length <= 280 // 2
            };
        });
    }
    handleSubmit() {
        if (!this.state.valid) {
            return;
        }
        const newPost = {   // 3
            content: this.state.content,
        };  
    }
    render() {
        return (
            <div className="create-post">
                <textarea
                    value={this.state.content}
                    onChange={this.handlePostChange}
                    placeholder="What's on your mind?"
                />
                <button onClick={this.handleSubmit}>Post</button>
            </div>
        );
    }
}

export default CreatePost;
```

## 5.3 Creating new posts

To send ur post up to the API, you'll need to do the following things, in addition to what the CreatePost component is already doing, which includes keeping track of state, doing some basic validation, and performing some basic content sanitization.

Next, you'll need to do the following to send data up to your API:

1. Capture the user input to be used as the post, updating state and perofrming data-checking logic you've implemented so far.
2. Call an event handler function passed from the parent component(App) as a prop and give the post data to it.
3. Reset the CreatePost component's state.
4. In the parent component, use the data passed from the CreatePost child component to perform an HTTP POST to the server.
5. Update the local component state with the new post you receive from the server.
6. To get a better grasp on what you'll be doing, see illustration in figure 5.5

listing 5.9 handling post submission (src/app.js)

```
import * as API from './shared/http';

//...

export default class App extends Component {
    //...
    createNewPost(post) {
        this.setState(prevState => {
            return {
                posts: orderBy(prevState.posts.concat(newPost),'date','desc')
            };
        });
    }
    //...
}
```

Listing 5.10 passing callback as props(src/app.js)

```
import * as API from './shared/http';
import CreatePost from './post/Create'; // 1

//...

export default class App extends Component {
    //...
    createNewPost(post) {
        this.setState(prevState => {
            return {
                posts: orderBy(prevState.posts.concat(newPost),'date','desc')
            };
        });
    }
    //...
    render() {
        return (
            //...
            <CreatePost onSubmit={this.createNewPost} />    // 2
            //...
        )
    }
    //...
}
```

## 5.4 SUMMARY

- Forms are handled like component.
- froms are just components
- form validation and sanitization work the same React mental model
- pass functions as props between componnets
- use regular js libs to validation and sanitization

next: integrate a third-party lib to add maps to your app.

# ch6: Integrating third-party libraries with React

covers
- sending form data in JSON format to a remote API
- Building some new kinds of components, including a location-picker, type-adhead, and a display map
- Integrating your app with Mapbox to search locations and display maps

work with jQuery, jQuery plugins

## 6.1 Sending posts to the letters-social api

refresh comments are gone.

keep everything local:
- cookies
- IndexedDB
- WebSQL

listing 6.1 send posts to server （app.js)

Lodash: 一个js实用工具库

Listing 6.2 calling functions passed via props

## 6.2 Enhancing your component with maps

using mapbox.com

### 6.2.1 DisplayMap component using refs

escape hatch 安全舱口 ： refs

refs to underlying DOM node

Listing 6.4 create a map with mapbox

Listing 6.5 A dynamic map(src/components/map/DisplayMap.js)

improvement: add static image of map, useful when using server-side rendering in ch12. user able to see a location for posts even before the app has fully loaded.

Listing 6.6 Adding a fallback map image

### 6.2.2 Creating the LocationTypeAhead component

a location type-ahead

Listing 6.7 beginning of LocationTypeAhead

mapAPI: Mapbox, Google Maps

Listing6.8 searching for location

Geolocatin API: ask people whether thet want to share their location.

Listing 6.9 Adding Geolocation

### 6.2.3 Updating CreatePost and adding maps to posts

subrendering

Listing 6.13 adding map to post

## 6.3 SUMMARY

- ref is a referencce to an underlying DOM element. Refs can be useful when you need an escape hatch and need to work with libs that work with DOM outside of React
- controlled or uncontrolled
- refs

next: add complexity to and create basic routing for app so you have the possibility of multiple pages.

// 2022 10 22

# ch7. Routing in React

## 7.1 What's ROUTING

Routing: a system for resource navigation.

### 7.1.1 Routing in modern front-end web app

The client-APP is sent down by the server and then effectively "takes over". The server is then responsible for sending down raw data, usually in form of JSON.

## 7.2 Creating a Router

- Router and Route components
- Router will be comprised of Route components 由Route组成Router
- Each Route will represent a URL path and map a component to that URL
- Router look like a normal React component
- The Route can  specify parameters like /users/:user, where the :user syntax will denote a value passed to the component
- You'll alse create a Link componnet that will enable navigation with your client-side router

Listing 7.1 Router end result (index.js)

a small, lightweight router library created by TJ Holowaychuk : react-enroute

### 7.2.1 Component routing

### 7.2.2 Creating the <Rout /> component

listing 7.2

### 7.2.3 Starting to build <Router/> component

#### What about React Router?

Listing 7.3 Scaffolding out the Router

Listing 7.4 cleanPath(Path)

normalizeRoute

Listing 7.5 normalizeRoute(path, parent)

### 7.2.4 Matching URL paths and parameterized routing

path matching 

enroute

express.js

Table 7.1 common routes

:name syntax

parameterized routing : 'path-to-regexp ' library

https://www.npmjs.com/package/path-to-regexp

Lissting 7.6 Finished Router

### 7.2.5 Adding routes to the Router component

enroute usage example : https://github.com/lapwinglabs/enroute

Listing 7.7 

opaque 不透明

children.forEach .count .only .toArray

#### Self-eradicating components in React

React 16 enable components to return arrays from render.

Listing 7.8 addRoute 

Listing 7.9 addRoutes

Listing 7.10 Finished Router

## 7.3 SUMMARY

- Routing in modern client app doesn't require you to perform a complete page reload. Instead, it can be handled with client-side applications like React. This can decrease browser load time and potentially server load too.
- React doesn't have a built-in routing lib. Instead you can pick one from community or build your own from scratch.
- React provides you with several utilities to work with the opaque children data structure. You can iterate over multiple components, check to see how many there are, and more.
- You can use the routing setup you created to dynamically change which children are rendered inside of a component. You're listening for changes in the browser's location and rendering using that data.

next: use your Router and add authentication to your app with Firebase

// 2022 10 22

# ch8 More routing and integrating Firebase

ccovers
- using the router built in ch7
- creating routing-related components like Router, Route, and Link
- Working with HTML5 History API to enable push-state routing
- Reusing components
- Integrating user authentication and Firebase

## 8.1 Using the ROUTER

history library: npm

To take advantage of history, you will need to refactor some of your components, which should give you a sense of the benefits of composability and modularity in React.

listing 8.1 refactoring to dynamically show children

### 8.1.1 Creating a page for a post

You are routing!

### 8.1.2 Creating a <Link/> component

accessibility:

WAI-ARIA authoring practices

MDN document on ARIA

Ari Rizzitano talk "Building Accessible Components"

Listing 8.7 Creating the link component

Listing 8.8 Integrating the link component (post.js)

### 8.1.3 Creating a <NotFound/> component

Listing 8.9 Creating the NotFound component pages/404.js

Listing 8.10 Adding individual posts to the router src/index.js

## 8.2 Integrating Firebase

enabling user login and authentication

"back-end as a service" Firebase.google.com

a drop-in replacement for a back-end API

https://console.firebase.google.com

Listing 8.11 Configuring the Firebase back end src/backend/core.js

Listing 8.12 Setting up authentication tools src/backend/auth.js

Listing 8.13

### 8.2.1 Ensuring a user is logged in

Listing 8.14 Adding the login container to the Router (src/index.js)

listing 8.15 Updating the Navbar component with src/components/nav/navbar.js

## 8.3 SUMMARY

- Firebase is a "back-end as a servece" tool that lets you authenticate users, store data, and more. It can get you pretty far without having to do any back-end development and is a great place to start for many hobby projects.
- You can integrate browser history APIs with your router. This also enables you to create Link components that don't require a full page reload in lieu of regular anchor tags.
- Firebase can handle authentication and user session data for you. We'll explore more advanced methods of handling changing state like this in later chapters when we look at Flux, Redux and eveen using Firebase on the server-side rendering.

next: testing

testing Ur React component using Jest and Enzyme.

// 2022 10 22

# ch9 Testing React components

covers:
- Testing front-end applications
- Setting up testing for React
- Testing React components
- Setting up test coverage

## 9.1 Types of testing

- Unit 
- Service
- Integration

testing pyramid

### 9.1.1 why test?

TDD
1. we want software work
2. testing help you write better code
3. integrating testing into software development workflow means you release code more frequently. shipping often!
4. tests help ou when go back and refactoring

Use **continuous integration** or **continuous deployment** tools like Circle CI, Travis CI or others.

recommand:

The Art of Unit Testing , second edition manning 2013 by Roy Osherove

Growing Object-Oriented Software: Guided by Test by Nat Pryce and Steve Freeman Addison-Wesley, 2000

## 9.2 Testing with JEST, ENZYME AND REACT-TEST-RENDERER

libraries used
- Test runner: Jest(facebook), Mocha, Jasmine
- Test doubles: other part mocked out ;Jest, Sinon
- Assertion libraries: Jest
- Environment helpers: Browser envinronment: Enzyme(airbnb), and the React test renderer.
- Framework-specific libraries: 
- Coverage tools: Jest's built-in coverage tool utilizes *Istanbul*(a popular tool)

## 9.3 Writing first tests

### 9.3.1 getting started with Jest

Tooling matters!

### 9.3.2 Testing a stateless functional componnet

assertion : Enzyme's shallow rendering

listing 9.4

Snapshot testing, visual regression testing

listing 9.5

### 9.3.3 Testing the CreatePost component without Enzyme

user flows, cross-browser testing:

QA team and SETs(software engineers in test)

higher level testing:

Selenium: https://www.seleniumhq.org

Puppeteer: https://github.com/GoogleChrome/puppeteer

Protractor: https://www.protractortest.org/#/

Listing 9.8 9.9 9.10

### 9.3.4 Test coverage

Istanbul

## 9.4 SUMMARY

- testing important
- Manual testing doesn't scale well
- Tools to test
- Unit Integration test
- Tools Enzyme
- Clean test: easy to read and well organized and use appropriate proportions of tests.

next: Redux architectural pattern

// 2022 10 23


























