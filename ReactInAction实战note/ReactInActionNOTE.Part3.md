# Part3. React application architecture

ch10, 11: explore Flux app architecture and implement Redux. 

ch12: server-side rendering, node.js server runtime. React Router

ch13: explore React Native

# ch10. Redux app architecture

- Redux actions, stores, reducers, and middleware
- Simple testing of Redux actions, stores, reducers, and middleware

Many approaches to build complex app with React are base on the Flux model.

Flux v.s. MVC architecture: promoting unidirectional data flow 单向数据流; introducing new concepts(dispatchers, actions, stores).

Redux : can be used with most js frameworks.

- core concepts
    - actions: represent work being done
    - middleware: allows you to inject custom behavior into process
    - reducers: determine how state should change
    - the store: holds a centralized copy of state
- integration of Redux

## 10.1 The Flux

MVC Model View Controller

Jeff Atwood: understanding mvc

#### MVC

Model-- data for you app

View-- a representation of your model :UI

Controller-- glue that binds the m and v together

#### Flux Redux

MVC: Ruby on Rails

Flux: 完全不同

- Store: app state and logic;
- Actions: Rather than update state directly, Flux app modify their state by creating actions that modify state.
- View: UI, usually React
- Dispatcher: A central coordinator of actions and updates to stores.

view -> actions -> dispatcher -> store -> view

actions are created from views.

dispatcher handles incoming actions.

actions are then sent to the appropriate store to update state.

state,having changed, notifies a view that new data should be used(if applicable). 

Part of the reason why MVC is difficult is that people generally aren't good at reasoning about change that occures over time.

keeping mental track of 异步 asynchronous chagnes to data over time is hard.

Flummox Fluxxor Reflux Fluxible Lux McFly MartyJS

### 10.1.1 Meet Redux

" a predictable state container for js app"

diffs between redux and flux
- Redux uses a single store
- Redux introduces reducers--Reducers are a more immutable approach to mutation. In Redux, state is changed in a predictable and deterministic 确定性的 way, one part of state at a time, and only in one place(the global store).
- Redux introduces mimddleware--inject custom behavior as data is updated.
- Redux actions are decoupled from the store.-- Action-creators don't dispatch anything to the store; instead, they return action objects that a central dispatcher uses.

overview of the architecture.

An action is created when you want to update state(click). The action will have a type that a certain reducer will handle. The reducer that handles the given actin type will make a copy of the current state, modify it with data from the action, and then return the new state. When the store is updated, view layers can listen to updates and respond accordingly.

### 10.1.2 Getting set up for Redux

To get set up to use Redux, you're going to need to do a few things:
- Make sure you've install dependencies, 'js-cookie','redux-mock-store' and 'redux'
- Install redux developer tools

Dan Abramov : Redux React

## 10.2 Create actions in Redux

action: a plain old js object(POJO) with a required type key and anything else you want.

Listing 10.1 some simple Redux actions

### 10.2.1 Defining action types

Listing 10.2 src/constants/types.js

URL-like fashion liike

### 10.2.2 Creating action in Redux

action creators-- functions that return an action object-- and dispatched by the store using dispatch function.

Listing 10.3 loading and loaded action creators (src/actions/loading.js)

### 10.2.3 Creating store and dispatch

root reducer file: allow you to create a store

Listing 10.4 creating root store (src/reducers/root.js)

store/store.js store.prod.js store.dev.js

Listing 10.5 creating Redux store

Llisting 10.6 dispatch src/store/exampleUse.js

Listing 10.7 

### 10.2.4 Asynchronous actions and middleware

*redux-thunk*： Express or Koa

10.8 eable redux-thunk

listing 10.9  creating the error action (arc/actions/error.js)

listing 10.10 creating comment actions (src/actions/comments.js)

listing 10.11 creator async and synchronous actins(ssrc/actions/posts.js)

listing 10.12 creating more post action creators

### 10.2.5 To Redux or not to Redux?

lsiting 10.13 create user-related actions(src/actions/auth.js)

async/await

### 10.2.6 Testing actions

Listing 10.14 Testing actions in Redux 

### 10.2.7 Creating custom Redux middleware for crash reporting

The central state object in Redux; source of truth: Store

Objects that contain chagne-related info. They must have a type and can contain any additiional info needed to communicate that sth happened.: Action

Functions used by Redux to compute changes to state based on sth happening.: Reducer

Fuctions that are used to create type and payload information about th happened in app.: action creator

listing 10.15 Creating simple crash-reporting redux midddleware

## 10.3 SUMMARY

- Redux for state management
- Redux enforces strict ways of working with data
- store : the source of truth
- Only one store in Redux
- Reducer(func) to compute changes.
- Redux v.s. Flux : 1 Reducer 2 action-creator don't directly dispatch actions
- actions: type + other info.
- action-creators: with certain middleware, you can create asynchronous action creators taht are useful for doing things like calling remote APIs
- Redux allow u to write middleware, a place for injecting custom behavior into the Redux state management process. Middleware is executed before reducers are fired off and allow you to perform side effects or implement global solutions for your app.

next: Redux, reducers and integrate them.

# ch11. More Redux and integrating Redux with React

covers:
- Reducers
- using Reducers
- Converting ur app to use Redux architecture
- adding like and comment functionality to your app

## 11.1 Reducers determine how state should change

just compute, must be a function

### 11.1.1 State shape and initial state

### 11.1.2 setting up reducers to respond to incoming action

Listing 11.2 setting up the loading reducer

Listing 11.3 Creating the comments reducer

#### Migrating to Redux: worth it?

Redux can be a lot of work to initially set up.

spend a month to migration from Flux to Redux, but they were able to launch the rewrite of the app with minimal instability and bug creation.

The greater overall outcome, howerver, was the ability to more rapidly iterate on the product due to the patterns that Redux helped us put in place.

What's more, the patterns Redux provided for us made it trivial 不重要 to add to the state of the application where necessary.

---------

Listing 11.5 creating the error reducer

listing 11.6 pagination reducer

listing 11.7 user reducer

### 11.1.3 Combining reducers together in our store

listing 11.8 adding new reducers to root reducer

### 11.1.4 Testing reducers

#### True of false

F F F T

-----------

## 11.2 Bring react and redux together

### 11.2.1 Containers vs. presentational components

presentational components : "UI-only" 
- They deal with how things look instead of how data flows or ins determinded.
- They only have their own state if neccesary; most of the time they should be stateless, functional components that receive props from Redux via react-redux bindings.
- When they do have their own state, it should be UI-related data, not app data. For example : an open/closed dropdown menu item and its state.
- They don't determine how data gets loaded or changed--that should happen primarily in containers.
- They're usually created "by hand" instead of by the react-redux lib
- They may contain style info, things like CSS classes, other style-related components, and any other UI-relatted data.

smart : containers ; dumb : presentational : wrong thinking about them.

container components:
- Serve as a data source and can be stateful; state usually come from your Redux store.
- Provide data and behavior info(like action) to presentational components.
- Can contain other presentational or container components; it's common for a container to be a parent with many presentational child components.
- Are usually created using react-redux's connect method and are usually higher-order components(components that create new components from other components).
- Usually don't have style info that doesn't have to do with app data. For example, the user profile state slice on the Redux store might have "red" recorded for the user's "favorite color", but the container wouldn't use that data for any styling-- it would only ever pass it down to a presentational component.

### 11.2.2 Using <Provider /> to connect components to the Redux store

listing 11.10 wrapping your app with <Provider/>

Listing 11.11 mapStateToProps

### 11.2.3 Binding actions to component event handlers

listing 11.12 using mapDispatchToProps 

## 11.2.4 Updating your tests

Listing 11.13 Updating the Home component test

## 11.3 SUMMARY

- Reducers are functions used by Redux to compute changes to state based on a given action.
- Redux / Flux: reducers, single store, and its action creators don't directly dispatch actions.
- state all lives in one area and can only updated through specific APIs
- action-creators
- middleware
- react-redux provides bindings for React components that enable you to connect your components to your store, handle the passing of new props, and check for updates from Redux.
- Container components are components that only deal with data and nothing UI-related.
- Presentational components are only concerned with what you can see or UI-specific data
-  Redux enforces a unidirectional data flow pattern where data are computed by reducers responding to actions and applied to the store.

next: server-side rendering 

// 2022 10 23

# ch12. React on the server and integrating React Router

covers:
- server-side rendering with React
- When to and when not to add server-side rendering to your app
- Transitioning your routing setup to React Router
- Handling authenticated routes with React Router
- Fetching data during server-side rendering
- Using Redux in the server-side rendering process

SSR: server-side rendering

## 12.1 What's SSR?

Ruby on rails or Laravel : SSR

WordPress, Ruby on Rails

### 12.1.1 Digging into server-side rendering

SSR use ERB(Embedded Ruby)

more: http://guides.rubyonrails.org/layouts_and_rendering.html

templating language: Handlebars, Jade, EJS, or React's JSX

## 12.2 why render on the server?

Learning more about thinking through different aspects of web performance, a great place to start is Google's Web Fundamentals guide:

https://developers.google.com/web/fundamentals/performance

## 12.3 You might not need SSR

There are at least a few reasons why integrating server-side rendering can add complexity:

- You'll need to synchronize the server and client in a way that your client can understand when it takes over. This can involve setting up markup, even handlers, and more that a client might need. Your authentication implementation will also need to account for requests coming from either the server or the client, which may require changes.
- coordinate handoff
- server and client both need to suport js.
- complex maintenance process

use only what you need!

Instagram doesn't seem to be using React to do SSR.

Netflix do.

## 12.4 Rendering components on the server

node.js runtime

Node.js in Action, 2nd Edition by Alex Young, Manning

Listing 12.3 basic server setup 

## 12.5 switching to react router

## 12.6 Handling authenticatedd routes with teact router

## 12.7 Server redndering with data-fetching

## 12.8 SUMMARY

- SSR is generating the static markup for a UI on a server that is sent to a client. SSR with React involves using React-DOM to either render an HTML string that React can reuse when running on the client-side or static markup that's meant to remain static on the browser.
- Not all js frameworks or libraries are built to handle SSR; React is and can "take over" markup that was generated on the server without having to initially re-render existing elements on the browser.
- Using a routing solution like React Router can allow you to share routes between the client and server, allowing you to share some code across platforms.
- SSR can be complex to implement and only makes sense in certain cases. Some situation where it might make sense include when you're especially concerned about SEO, when you have an app whose critical path needs to involve a quick first paint, or if you're using React as a static markup generator.
- The performance gains SSR can offer are often only realized if the page payload sent down by a server is not overly large (so as to not take even longer to load than before). A longer response time and more data may obviate the quick first paint you would otherwise get.
- SSR requires you to consider which parts of your app will work on the server and which don't. Those features that require a browser environment need to be patched to work or should be handdled so as not to run on the server.
- You can accomplish a "complete" render on the server by doing work to synchronize authentication state between client and server and doing any necessary fetching of data on the server.
- Although other js platform implementations exist, SSR practically requires you to run a node.js server or at least call out to one to generate your HTML for sending to the client.

next: brief look at React Native 

# ch13. An intro to RN

covers:
- overview of RN
- Diffs between React and RN
- ways to learn more about RN

We've been over the basics of using React, implemented a router, explored Redux, looked at server-side rendering, and even transitioned to using React Router.

## 13.1 intro RN

3 ways
- native
- hybrid(using webview)
- RN

RN: "really native" but you can use a combination of js and platform-specific code(Swift and Java)

Top-level features of RN:
- With RN, you can wirte js app that can also use native code and compile to native app that runs on mobile.
- RN can handle creating the same UI elements on mobile, potentially simplifying the dev of mobile app
- add native code when u need to, not constrained to js.
- RN share idioms with React.
- dev tool allows u to relaod without recompiling cycle
- share code and target multiple platforms
- share logic and styles

Listing 13.1 RN example

## 13.2 React and RN

- Runtime--React heavily uses the browser-specific APIs. RN use different layout and styling semantics. Things like threading, CPU utilizatin and others.
- Core APIs--Same:lifecycle, state, props; diff: networking, layout, geolocatin, resource management, persistence, events, and others.
- Components--RN built-in components
- Use of React core library
- lifecycle methods
- event types
- styling 
- third-party dependencies
- distribution: Xcode for iOS, "walled garden" nature of ios and android tooling
- Dev tooling: RN has a focus on hot reloading that isn't part of React by default.

## 13.3 When to use RN

- Solo developer--React to RN, if you aren't deeply experienced with native devlopment
- Small cross-functinal team--easily move engineers between native and web
- Team with little to moderate native expertise
- Deep native expertise

llimitations :
- Use of JS
- specific performance needs: no
- Highly specialized app: AR, graphic: no
- Internal application: suited

## 13.4 The simplest "hello world"

## 13.5 Where to go next

Learn once, write anywhere!

RN in Action by Nader Dabit, Manning 2018

create-react-native-app project

## 13.6 SUMMARY

recap:
- RN is a technology to write mobile app
- RN use core lib to create component, but use other lib to handle rendering and interaction
- RN handles bridging between js and mobile
- RN use APIs are similar or identical to web. Flexbox, Fetch;
- can mix js and native code
- RN provide robust set of tools for dev
- RN hot-reload tools
- Using RN can help lower the barrier to mobile development for you and your team
- RN be sufficient for most typical mobile app, but not every type of app

// end 2022 10 24















