# Problems with using only vanilla JS

The problems with using vanilla JS are.

1. Requires lot of direct DOM manipulation and traversing. This could end up in spaghetti code situaton.
2. Data (state) is usually stored in DOM, shared across enitire app. This can introduce many bugs in our application.

# Why do front-end framework exists?

- Keeping a user interface in sync with data is really hard and a lot of work. Front-end frameworks solve this problem and take hard work away from developers.
- They enforce a correct way of structuring and writing code(therefore contributing to solving the problem of spaghetti code).
- They give developers and teams a consistent way of building front-end applications.

# React vs. Vanilla Javascript

# What is React?

React is a JS library for building UI. React is an extremely popular, declaritive, component-based, state-driven JS library for building UI, created by facebook.

React is all about components. Components are the building blocks of UIs in React. All react does is to take components and draw them on the webpage. We build complex UIs in react by building multiple components and the combining them like lego pieces. Another thing that we can do with components is to re-use them.

We describe how components look like and how they work using a declarative syntax called JSX. Which means telling React what a component should look like, based on current data/state. React is abstraction away from the DOM. we bever touch the DOM. JSX is a syntax that combines HTML, CSS, JS as well as referencing other components.

The main goal of React is to constantly keep the UI in sync with the data(state). Based on the initial state react will rende the UI. Now on any action such as a button click the state will change. Whenver the state changes we will manually update the state and React will automatically re-render the UI based on the new state. Basically react will react to the state update.

React is a framework or library? React is a library, beacuase React is only the view layer. We need to pick multiple expernal libraries to build a complete application. Frameworks that complete all the missing functionality over React is NextJs, Remix etc.

React was created in 2011 by Jordan walker an engineer working on facebook at the time.React was open-sourced in 2013, and has since then completely transformed front-end web development.

React is good at 2 things:

1. Rendering components on a webpage based on their current state.
2. keeping the UI in sync with state by re-rendering(reacting) when state changes.

# Setting Up React App

We can set up react app by using create-react-app or vite.

- create-react-app is a `starter-kit` for react applications. Here, everything is already configured. ESLint, prettier, jest, etc. The issue with create-react-app is that it is slow and outdated therefore it is not recommended to use this for real-world app setup. However can be used to set up react for tutorials or experiments.

- vite is a modern build tool that contains a template for setting up React applications. With vite we need to manually set up ESLint, jest, prettier etc. The reason for using vite instead of create-react-app even if we have to manually set up everything is that it is extremely fast to automatically refresh the page when code changes. Also bundling is extremely fast with vite.

React team now advises to use `React framework` for new projects.(NextJs, Remix etc).
React framework is basically a framework build on top of react library.
