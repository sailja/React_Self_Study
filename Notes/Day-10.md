# How React works behind the scenes

## Component vs Instance vs Element

COMPONENT:

- Description of a piece of UI
- A component is a function that returns React elements, usually written in JSX
- Blueprint or template

INSTANCE:

- Instances are created when we use components
- number of time a component is used is the number of times its instance is created
- Actual or physical manifestation of a component in a component tree.
- Each instance has its own state and props
- Each instance has its own lifecycle

ELEMENT:

- JSX is converted to React.createElement() function calls which returns elements
- It basically contains all the information necessary to create DOM elements for the current component instance.
- Each element will be converted to DOM elements and will be painted on the UI
- Actual visual representation of the component instance in the browser

## How Rendering works

As we build our applications we build a bunch of components and then we use these components one or many times in other components. This creates 1 or more ccomponent instances for each component. Now, as React calls each component instance will produce a bunch of React.createElement function calls which will produce a react elements for each component instance, These react elements will get converted to DOM elements and then will finally be shown on the UI.

The question here is how the elements are displayed on the screen. The followings steps are the answer to the above question.

- First the render is triggered by updating state somewhere.
- React calls component functions and figures out how DOM should be updated (Render phase)
- Once react knows what to place in the DOM. It actually writes to the DOM, updating, inserting and deleting elements in the `Commit phase`
- Now, the browser will notice that the DOM has been updated so it re-paints the screen.

In React, rendering is NOT updating the DOM or displaying elements on the screen. Rendering only happens internally inside react. It does not provide visual changes.

### Render trigger phase

The two situations that triggers renders are:

1. Initial render of the application
2. When State is updated in one or more component instances (re-render).

The render process is triggered for the entire application
In practice, It looks like React only re-renders the components where the state update happens, but thats not how it works behind the scenes.
React looks at the entire tree once a render happens. Renders are not triggered immediately, but scheduled for when the JS engine has some free time. There is also batching of multiple setState calls in event handlers.

### The Render Phase

At the beginning of the render phase react will go through the entire component tree take all the component instances that triggered re-render and then render them.

This will create updated react elements which all together make-up the new virtual DOM

#### VIRTUAL DOM

It is a tree of all the React elements created from all instances in the component tree. It is cheap and fast to create multiple trees because it is just a JS object.

Now consider a state update in a component. React re-renders that component and all of its child components and create a new virtual DOM. Rendering a component will cause all of its child components to be rendered as well(no matter if props changed or not). This is necessary because React does'nt know whether children will be affected. But this does not mean thjat the entire DOM is re-reacted. Only a new virtual DOM will be created.

This new virtual DOM will then be reconciled (reconciliation + Diffing) with the current fiber tree(before state update). This is done in react reconciler called `Fiber` (therefore it is called fiber tree). After the reconsiliation a new updated Fiber tree is created.

Now you might be thinking why go through all this trouble of reconciliation and fiber tree why not update the entire DOM when state changes somewhere in the app
? The answer is simple that it would be inefficient and wasteful.

1. Writing to the DOM is slow
2. Usually only a small part of the DOM needs to be updated

React reuses as much of the existing DOM as possible. React finds out which elements have changed in the DOM by the process of reconciliation.

RECONCILIATION:

Deciding which DOM elements actually need to be inserted, deleted or updated in order to reflect the latest state changes.

This is processed by reconciler. Reconciler is basically the engine of react.The reconciler that allows us to never touch the DOM directly and tells react what the next snapshot of the uI should look like based on state. The current reconciler in react is called `Fiber`

On the initial render It takes the entire element tree and builds another tree called the fiber tree. Fiber tree is the internal tree that has the fiber for each component instance and DOM element. Fibers are NOT re-created on every render it just gets updated based on the re-renders. The rendering process can be performed asynchronously that means rendering process can be split into chunks , tasks can be prioritizes and work can be paused, re-used or thrown away
It enables concurrent features like suspense or transitions. ALso long renders won't block JS engine

### The Commit phase

The commit phase is where react finally writes to the DOM. From the render phase we get the list of DOM updates. React writes to the DOM. Commiting is synchrounous. DOM is updated in one go, it can't be interupted. This is necessary so that the DOM never shows partial results, ensuring a consistent UI (in sync with state at all times)

After the commit phase completes, the workInProgress fiber tree(new updated fiber tree) becomes the current tree for the next rende cycle this is because fiber tree are never discarded they are always re-used. After this the UI screen is updated

The render phase is done by the react library and the UI update is done by the browser but who takes care of the commit phase. The commit phase is done by a separate library called ReactDOM. React can be used by many hosts(platforms) like React native, remotion and many others.

### How Diffing works

Diffing uses 2 fundamental assumptions (rules):

1. Two elements of different types will produce different trees.
2. Elements with a stable key prop stay the same across renders

Diffing is comparing elements step by step between 2 renders based on their position in the element tree. There are 2 situations that needs to be considered

1. Same position, Different element

In case the element in a certain position is changed from div to header in that case -

- React assumes entire sub-tree is nmo longer valid
- Old components are destroyed and removed from DOM, including state
- Tree might be rebuild if children stayed the same (state is reset)

2. Same Position, Same element

   In case the element in a certain position is same but only its className changes -

- Element will be kept (as well as child elements), including state
- New props/ attributes are passed if they changes between renders
- This is something which we don't always want. And to avoid this we use the `Key` prop

### What is the Key prop?

- Key prop is a special prop to tell the diffing algorithm that an element is unique
- Allows react to distinguish between multiple instances of the same component type
- When a key stays the same across renders, the element will be kept in the DOM (even if the position in the tree changes)
- When a key changes between renders, then the element will be destroyed and a new one will be created (even if position in the tree is the same as before)
