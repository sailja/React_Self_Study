# Effects and Data Fetching

## The Component Lifecycle

The lifecycle of a component basically encompases the different phases that a specific component instance can go through over time.

1. MOUNT / Initial Render:

   - Component instance is rendered for the first time.
   - Fresh state and props are created

2. Re-Render

   - Happens when state changes, props changes, parent re-renders or context changes

3. Un-Mount:

   - Component instance is destroyed or removed
   - State and props are destroyed

We can define code to run at these specific phase

## UseEffect Hook

The idea of a useEffect hook is to give us a place where we can safely write side-effects. The side effects registered with the useEffect hook will only be executed after certain phases like the initial renders

There are 2 parts of the use effect hook, first is the function that contains the code (side effect) that we want to execute and the second one is the dependency array. Here in the below example we have the dependency array empty that means that the effect will be executed only once after the component is rendered.
Adding any dependency in the dependency array will cause the effect to be executed each time the dependency gets updated

Syntax:

```

useEffect(() => {
		fetch(`http://www.omdbapi.com/?apikey=${KEY}&s=matrix`)
			.then((res) => res.json())
			.then((data) => setMovies(data.Search));
	}, []);
```

### Event handlers vs Effects(useEffect)

Event Handlers:

1. Executed when the corresponding event happens
2. Used to react to an event

Effects:

1. Executed after the component moubts(initial render), and after subsequent re-renders (according to dependency array)
2. Used to keep a component synchronized with some external system

### What is UseEffect Dependency array?

By default effect run after every render. We can prevent that by passing a dependency array

Without the dependency array, React doesn't know when to run the effect
Each time one of the dependences changes, the effect will be executed again.

Every state variable and prop used inside the effect MUST be included in the dependency array. Otherwise we get a `stale closure`.

### The mechanics of effects

UseEffect is like an event listener that is listening for one dependency to change. Whenever a dependency changes, it will execute the effect again

Effects react to updates to state and props inside the effect(the dependencies). So effects are `reactive`(like state updated re-rendering the UI)

We can use the dependency array to run effects when the component renders or re-renders

There are 3 ways to define dependency arrays

```
useEffect(fn, [x, y, z]); ---> Effect synchronizes with x, y and z. Runs on mount and re-renders triggered by updating x, y or z.

useEffect(fn, []) ----> Effect synchronizes with no state/props. Runs only on mount(initial render)

useEffect(fn) ---> Effect synchronizes with everything. Runs on every render (usually bad and should be avoided)
```

### When are Effects executed

Mount (initial render)---> Commit ---> Browser paint ---> Effects

the reason for effects being executed after browser paint is that effects may contain long running processes such as fetching data. In a situation like that if react will run the effect before browser paint it will block this enitire process and users will see an old version of the component for way too long. If an effect sets state, an additional render will be required this is why we should not over use effects

If we want to run effect before browser paints the screen we can use useLayoutEffect but we should generally avoid that
