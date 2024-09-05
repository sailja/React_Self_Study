# Handling Events in React

In react we don't use addEventListener. We can simply use the eventName on the element itself. Like in the below example the onClick method. The onClick is the event listener and when we click on the button the function in all click gets executed. One thing to keep in mind is that never call a function in eventhandler. Always specify a function value

```

<button style={{ background: '#7950f2', color: '#fff' }} onClick={() => alert('previous')}>Prev</button>

```

# What is State in react?

In order to make component interactive we need state. Everything keeps revolving around state in react.

Data that a component can hold over time, necessary for information that it needs to remember throughout the apps lifecycle. State is basically used to store data for a particular component. We can also say that state is a components memory. State is mutable.

`State variable/ piece of state` is a single variable in a component on the other hand `state` is all the state variables together.

Updating component state triggers React to re-render the component. State allows developers to do 2 thiings:

1. Update the components view (by re-rendering)
2. Persist local variables between renders

Understanding the mechanics of state will unlock the power of react development.

Let us understand state with a small example. In the below code we want to update the step count on clicking previous or next button and change the view for the text. How do we do that. We can create a state variable using useState hook that takes an argument as the default value of the state variable. Here we are passing 1 as the default value. The useState returns an array with 2 values. The first value is the actual value that we store(step) and the second one is a set method(setStep) that is used to set the state or to update the state.

Here useState is a React hook and hooks can only be called at the top level of the component and we cannot call hooks conditionally.

```
export default function App() {
    //Setting the default value as 1 for the step state variable
	const [step, setStep] = useState(1);

	const handleNext = () => {
		setStep(step + 1);
	};
	const handlePrev = () => {
		setStep(step - 1);
	};
	return (
		<div className='steps'>
			<div className='numbers'>
				<div className={`${step >= 1 ? 'active' : ''}`}>1</div>
				<div className={`${step >= 2 ? 'active' : ''}`}>2</div>
				<div className={`${step >= 3 ? 'active' : ''}`}>3</div>
			</div>
			<p className='message'>
				Step {step}: {messages[step - 1]}
			</p>
			<div className='buttons'>
				<button
					style={{ background: '#7950f2', color: '#fff' }}
					onClick={handlePrev}
				>
					Previous
				</button>
				<button
					style={{ background: '#7950f2', color: '#fff' }}
					onClick={handleNext}
				>
					Next
				</button>
			</div>
		</div>
	);
}

```

We should not set state manually without using the setState function. Like doing `step = step + 1` won't work. The reason is react won't know that the state is being updated and therefore the view won't get updated. Therefore always use setState method(here setStep) to update the state variable.

## Mechanics of State

In react we do not manipulate the DOM directly. Then how do we update the component view ? To understand this we need to understand another aspect.

In react a view is updated by re-rendering the component. Re-rendering basically means that React calls the component function again. React preserves the state throughout re-renders.
When state is updated the entire component gets re-rendered.
In the above example we can see that each time we click the next or prev button the enitre component gets re-rendered with the new data.

React reacts to state changes by re-rendering the UI

### React Developers Tools

To use react dev tools add the react dev tools extension on chrome.This is very helpful in debugging code.

There are 2 parts in dev tools

1. Components
2. Profiler

Components basically shows us the entire component tree and on clicking a particular component we can see the props and state for that component. The state is visible under hooks. You can manipulate the value of the state on the dev tools for testing purpose.

## Updating state based on Current state

```
const [step, setState]  = useState(1);


setState(step + 1);
setState(step + 1);
```

This will work but what if we want to set the state twice? Even if we call setState twice it will still update the value once.
For the above example the value of step will be 2 and not 3.
How to make it work then?

There is a simple way of doing it. Instead of directly using the current state value we can use a callback function with previous state as argument and then we can update the state based on the previous state just as shown in the below example

```
const [step, setState]  = useState(1);


setState((prevState) => prevState + 1);
setState((prevState) => prevState + 1);
```

This will update the state twice

## One Component, One State

Each component has and manages its own state, no matter how many times we render the same component. For example if we use a single component thrice then each of those components will have their separate state and updating the state in 1 won't affect the other.

## UI as a function of state

The entire UI is always a represention of all the current states in all the components. React app is fundamentaly updating state over time also correctly displaying correct state all the time.
With state we view UI as a reflection of data changing over time. We describe that reflection of data using state, event handlers and JSX.

## Practical guidelines about state

- Use a state variable for any data that the component should keep track of over time. This is data that will change at some point. In Vanilla JS, that is a let variable or an [] or {}.

- Whenever you want something in the component to be dynamic, create a piece of state related to that thing and update the state when the thing should change.
  Example- A modal windoe can be open or closed. So we create a state variable isOpen that tracks whether the modal is open or not. On isOpen = true we display the window and on isOpen = false we hide it.

- If you want to change the way a component looks, or the data is displayed, update the state. This usually happens in an event handler function.

- When building a component, imagine its view as a reflection of state changing over time

- For data that should not trigger component re-renders, don't use state. Use a regular variable instead. This is a common beginner mistake.
