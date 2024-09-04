## Rules of JSX

### General rules

- JSX works essentially like HTML, but we can enter `javascript mode` by using {} (for text or attributes)

- We can place any JS expression inside {}. e.g. reference variable, create arrays or objects, [].map(), ternary operator

- Statements are not allowed (if/else, for, switch)

- JSX produces a JS expression

- A pice of JSX only have one root element. If you need more, use <React.fragment> (or the short <>)

## Difference between JSX and HTML

- Classname instead of HTML's class

- htmlFor instead of HTML's for

- Every tag needs to be closed. e.g. <img /> or <br />

- All event handlers and other properties need to be camelCased. e.g. onClick or onMouseOver

- Exception: aria-_ and data-_ are written with dashesh like in HTML

- CSS inline styles are written like this : `{{<style>}}` (to reference a variable and then an object)

- CSS property names are also camelCased

- Comments need to be in {} (because they are JS)

## Rendering lists

Rendering list meaning we have an array and we want to create a component for each component in the array.
Using the component manually one by one is not always a good idea. We can simply use the map function in our JSX as shown in the below example. Here we are basically rendering pizza component for each pizza data that we have using the map function

```
function Menu() {
	return (
		<main className='menu'>
			<h2>Our Menu</h2>
			<ul className='pizzas'>
				{pizzaData.map((pizza) => (
					<Pizza
						pizza={pizza}
						key={pizza.name}
					/>
				))}
			</ul>
		</main>
	);
}

function Pizza(props) {
	const { name, ingredients, price, photoName, soldOut } = props.pizza;
	return (
		<li className='pizza'>
			<img
				src={window.location.origin + photoName}
				alt={window.location.origin + pizzaData[2].photoName}
			></img>
			<div>
				<h3>{name}</h3>
				<p>{ingredients}</p>
				<span>{soldOut ? 'Sold out !!!' : price * 30}</span>
			</div>
		</li>
	);
}
```

## Conditional rendering

### Conditional rendering with &&

There can be scenarios in which you want to render a component based on a certain condition. In that case we can simply use conditional rendering using && operator because of short-circuiting. In the below example we can see that the `<p>` or the message will only get rendered if the isOpen variable is true.

```
function Footer() {
	const hour = new Date().getHours();
	const openHour = 12;
	const closeHour = 22;
	const isOpen = hour > openHour && hour < closeHour;
	const message =
		hour > openHour && hour < closeHour
			? 'We are currently open!'
			: 'Sorry! We are currently closed';


	return <footer className='footer'>{isOpen && <p>{message}</p>}</footer>;
}
```

### Conditional rendering with ternary operator

The ternary operatoe is used when we want to use if else in order to show components i.e. if condition satisfies then component 1 else component 2. We read earlier that if-else statements cannot be used in JSX so to achieve the same functionality we use ternary operator. This can simply be understood using the below example. Here we are basically rendering the `'We are currently open!'` when isOpen variable is true and `'Sorry! We are currently closed'` when isOpen is false.

```
function Footer() {
	const hour = new Date().getHours();
	const openHour = 12;
	const closeHour = 22;
	const isOpen = hour > openHour && hour < closeHour;

	return (
		<footer className='footer'>
			{isOpen ? (
				<p>{'We are currently open!'}</p>
			) : (
				<p>{'Sorry! We are currently closed'}</p>
			)}
		</footer>
	);
}
```

### Conditional rendering with multiple returns

Till now we saw only one return keyword used in all of our components. But we can always add multiple return keywords based on certain conditions. Our component will still return one JSX element but that will depend on the condition. The same code mentioned in the above example can be written using ultiple returns as mentioned below.

```
function Footer() {
	const hour = new Date().getHours();
	const openHour = 12;
	const closeHour = 22;
	const isOpen = hour > openHour && hour < closeHour;
	if (!isOpen) {
		return (
			<footer className='footer'>
				<p>{'Sorry! We are currently closed'}</p>
			</footer>
		);
	}
	return (
		<footer className='footer'>
			<p>{'We are currently open!'}</p>
		</footer>
	);
}
```

## Extracting JSX into a New Component

It basically means breaking up long JSX into smaller components and using it in the main component. The above example can be simply modified by creating separate components for both the return JSX and then returning the new components in the if else. This is just to make code cleaner and more readable.

## Destructuring Props

Each time that we pass props to a component that component will then recieve a new object containing all the props passed to it. To avoid having to write props.xyz everytime we want to use a prop we use destructring props. Since props is an object we can destructure it same way as we destructure an object

```
function Pizza(props) {
    //destructed props
	const { name, ingredients, price, photoName, soldOut } = props;
	return (
		<li className='pizza'>
			<img
				src={window.location.origin + photoName}
				alt={window.location.origin + pizzaData[2].photoName}
			></img>
			<div>
				<h3>{name}</h3>
				<p>{ingredients}</p>
				<span>{soldOut ? 'Sold out !!!' : price * 30}</span>
			</div>
		</li>
	);
}
```

this can also be done right in the function argument by writting exactly the name of the object that we passed in just as done in the below example. One thing to keep in mind is never ever miss the curly braces

```
function Pizza({ name, ingredients, price, photoName, soldOut }) {

	return (
		<li className='pizza'>
			<img
				src={window.location.origin + photoName}
				alt={window.location.origin + pizzaData[2].photoName}
			></img>
			<div>
				<h3>{name}</h3>
				<p>{ingredients}</p>
				<span>{soldOut ? 'Sold out !!!' : price * 30}</span>
			</div>
		</li>
	);
}
```

## React Fragments

As we learned in the rules for JSX. JSX element no matter where ever defined can only have 1 root element in that case we use fragments. Let us understand with the example. In the first example react will throw error because there are 2 root elements in the JSX (img and div), but as per the rules there can be only one root element in this case we can wrap this code in fragment (React.Fragment or <>) just as we have done in the second example

```
//Example-1 :
function Pizza({ name, ingredients, price, photoName, soldOut }) {

	return (

			<img
				src={window.location.origin + photoName}
				alt={window.location.origin + pizzaData[2].photoName}
			></img>
			<div>
				<h3>{name}</h3>
				<p>{ingredients}</p>
				<span>{soldOut ? 'Sold out !!!' : price * 30}</span>
			</div>

	);
}

//Example-2:
function Pizza({ name, ingredients, price, photoName, soldOut }) {

	return (
        <>
			<img
				src={window.location.origin + photoName}
				alt={window.location.origin + pizzaData[2].photoName}
			></img>
			<div>
				<h3>{name}</h3>
				<p>{ingredients}</p>
				<span>{soldOut ? 'Sold out !!!' : price * 30}</span>
			</div>
         </>

	);
}

//OR

function Pizza({ name, ingredients, price, photoName, soldOut }) {

	return (
        <React.Fragment>
			<img
				src={window.location.origin + photoName}
				alt={window.location.origin + pizzaData[2].photoName}
			></img>
			<div>
				<h3>{name}</h3>
				<p>{ingredients}</p>
				<span>{soldOut ? 'Sold out !!!' : price * 30}</span>
			</div>
         <React.Fragment />

	);
}

```
