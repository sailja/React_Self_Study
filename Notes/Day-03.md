# Components, Props, and JSX

## Setting up the first index file in the your react project

This is the main file in the src. when we create out own react project after running the create-react-app or vite simply delete all the files from src and create an index.js file with the below mentioned code. It is the base page or the main page of our react project. We will be modifying this file further as per our requirements.

```
import React from 'react';
import ReactDOM from 'react-dom/client';

function App() {
	return (
		<div>
			<h1>React Pizza</h1>
		</div>
	);
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<React.StrictMode>
		<App />
	</React.StrictMode>
);
```

## Components

Components are the most fundamental concept in react. Simply because:

- React applications are entirely made out of components
- Building blocks of user Interface in react
- Each component has its own data, loogic and appearance (how it works and looks)
- We build complex UIs by building multiple components and combining them.
- Components can be reused, nested inside each other and pass data between them

React renders a view for each component and then all these views together make the UI. Component is basically a piece of UI.

### Creating a component

In react we create components using functions. There are 2 imp rules when writing a component as functions

- function name should start with upper case letter
- funtion should return a markup

```
function Pizza() {
	return <h2>Pizza</h2>;
}

```

In order to call a react component we use the same syntax as that of an html element.

```
<Pizza />
```

A component is reusable.

## What is JSX ?

JSX is a declarative syntax to describe what components look like and how they work.
Components must return a block of JSX.
Expension of JS that allows us to embed JS, CSS and React components into HTML.

Here a questions comes into picture that if react is a JS framework how will it understand the HTML looking code.
Remember that JSX is an extension of javascript. Which means there is a simple way to convert JSX to jS. This is done by a tool called babel which is automatically included when we did create-react-app.
Each JSX is converted to a React.createElement function call.

We can use react without JSX but then we will have to use React.createElement every time.

JSX is declarative. In an imperative approach like the one use vanilla JS we manually select element traverse the DOM and add event listeners. Basically we give step-bystep DOM mutations until we reach the desired UI. However in decalrative approach we describe how the UI should look like using JSX, based on current data. All this happens without DOM manipulation at all.

React is an abstraction away from DOM: we never touch the DOM
Instead we think of UI as a reflection of the current data.
JSX combines HTML, JS and CSS in a single block of code

## Separation of concerns

Before SPAs we has separate files each for JS, css and HTML this was the traditional separation of concern. As pages got more interactive they became SPA and JS became more inchanrge of HTML.
Since the logic and the UI became tightly coupled then what was the point of keeping them separated. Therefore react components started using jsx. This is why React contains data logic and appearance in a single file.

## Props

Props is essentially how we pass data between components, in particular from parent to child components.

In the below example we have 2 components `pizzas` and `menu`. Here menu is the parent component and pizzas is the child component. In order to pass data to the child component we use props. In the below example we are passing name, ingredients and other details as props to the `pizzas` component. In order to recieve the props in the pizza component we use the argument `props` in the pizzas component. `props` is basically an object containing all the details passed as props from the parent component and it can be used as props.name etc to show the details.

```
function Pizza(props) {
	return (
		<div className='pizza'>
			<img
				src={window.location.origin + props.photoName}
				alt={window.location.origin + pizzaData[2].photoName}
			></img>
			<div>
				<h3>{props.name}</h3>
				<p>{props.ingredients}</p>
				<span>{props.price + 3}</span>
			</div>
		</div>
	);
}

function Menu() {
	return (
		<main className='menu'>
			<h2>Our Menu</h2>
			<Pizza
				name='Pizza Salamino'
				ingredients='Tomato, mozarella, and pepperoni'
				photoName='/pizzas/salamino.jpg'
				price={15}
			/>
		</main>
	);
}
```

Props are an essential react tools to configure and customize components (like function parameters). With props, parent control how child components look and work. Anything can be passes as props: single values, arrays, objects, functions, even other components. Props are read-only (immutable). If we want to mutate props we need state.

Props are just objects if we change props in child component it will affect the parent component as well creating side effects(not pure). React is all about pure components to optimize apps and avoid bugs. Therefore props are immutable.

### One way data flow

In React applications data can only be passed from parent to child components (mainly through props) and not the opposite.
It makes applications more predictable and easier to understand.
Makes application easy to debug, as we have control over the data. This makes the app more performant.

There can be scenarios we would want to pass data to the parent component from child. There is a very clever way of doing this in react which we will be learning further
