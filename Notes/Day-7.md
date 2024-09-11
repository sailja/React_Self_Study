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

When a piece of state needs to be shared among multiple siblings in that case we need to define that state in the first parent component and then pass it as props to all the sibling components. This is called lifting up the state. and we also pass the setState method to one of the sibling component as a prop in order to update the state on some operation.
