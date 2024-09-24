## Thinking in React

Thinking in react is a process required to follow in order to build a react application

- Break the desired UI into components and establish the component tree
- Build a static version in react (without state)
- Think about state:
  - When to use state
  - Types of state: local vs. global
  - Where to place each piece of state
- Establish data flow:
  - one-way data flow
  - child to parent communication
  - accessig global state

Steps 3 and 4 is called state management which we will be learning in detail further

## When you know how to "Think in react" you will be able to answer the following questions

- How to break up a UI design into components?
- How to make some components reusable?
- How to assemble UI from a reusable component?
- What pieces of state do I need for interactivity?
- Where to place state?

## Fundamentals of state management

State management is deciding when we need to create pieces of state, what types of states are necessary, where to place each state and also how all the data will flow through the app.

### Types of state (local vs global)

Local state:

1. State needed only by one of few components
2. State that is defined in a component and only that component and child components have access to it (by passing via props)
3. We should always start with local state

Global state:

1. State that many components might need.
2. Shared state that is accessible to every component in the entire application. (context API or Redux)

### State: When and where

#### WHEN

need to store data ---> will data change at some point ---> NO --->
Regular const variable

need to store data ---> will data change at some point ---> YES --->
Can be computed from existing state/props? ----> YES ---> Derive state

need to store data ---> will data change at some point ---> YES --->
Can be computed from existing state/props? ----> NO ---> Should it re-render component? ---> place a new piece of state in the component

#### WHERE

need to store data ---> will data change at some point ---> YES --->
Can be computed from existing state/props? ----> NO ---> Should it re-render component? ---> place a new piece of state in the component ---> Only used by this component? ---> YES ---> Leave in component

need to store data ---> will data change at some point ---> YES --->
Can be computed from existing state/props? ----> NO ---> Should it re-render component? ---> place a new piece of state in the component ---> Only used by this component? ---> NO ---> Also used by a child component? ---> YES ----> pass to child via props

need to store data ---> will data change at some point ---> YES --->
Can be computed from existing state/props? ----> NO ---> Should it re-render component? ---> place a new piece of state in the component ---> Only used by this component? ---> NO ---> Also used by a child component? ---> NO ----> Used by one or a few sibling components ---> YES----> Lift state up to first common parent

## Lifting state up

When a piece of state needs to be shared among multiple siblings in that case we need to define that state in the first(closest) common parent component and then pass it as props to all the sibling components(whereever needed). This is called lifting up the state. and we also pass the setState method to one of the sibling component as a prop in order to update the state on some operation.

### Data flow between parent and child

Data flows from parent component to child component via props. This is called one way communication. We cannot pass data from child to parents via props. There can be scenarios where we might need to pass data from child to parent. This can be done by the child component updating the parent state. In order to achive this we simply pass the parent component setState to the child via props and then update the state in the child component. This is called inverse data flow.

## Derived State

Derived state is the state that is computed from an existing piece of state or from props. They are just like regular variable and no useState.

## Children Prop

Children prop is basically any jsx markup sent to the component by the parent. To pass these children instead of immediatly closing that component we can then write some more jsx in the component similar to how we write child elements in html element (Shown in below example where we are using the button component). This JSX can be accesed in the button component by using `props.children` in the JSX of the Button component

```
function Button({ textColor, backgroundColor, onClick, children }) {
	return (
		<button
			style={{ background: backgroundColor, color: textColor }}
			onClick={onClick}
		>
			{children}  //USING THE CHILDREN PROP
		</button>
	);
}

<Button
							textColor='#fff'
							backgroundColor='#7950f2'
							onClick={handleNext}
						>
							<span>Next</span> 👉  //PASSING CHILDREN PROP
						</Button>
```

- The children prop allows us to pass JSX into an element (besides regular props)
- Essential tool to make reusable and configurable components (especially component content)
- Really useful for generic components that don't know their content before being used (e.g. modal)
