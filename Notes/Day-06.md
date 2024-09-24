## Controlled Elements in React

By default the input fields maintain their own state inside the dom (inside html element itself). It makes very hard to read their values and also leaves the state in the dom which is not ideal. In react we keep all the state in one location i.e. inside react application and not the dom. In order to do that we use a techinque called controlled elements. In this technique it is react who controls and owns the state of the input fields and not the dom.
In order to follow the controlled technique there are 3 steps.

- first we create a state using the useState hook
- We specify the value using the created state to the input field(element)
- We set the state on change of value in the input field (on the input field/element using the onChange event)

```
function Form() {
	const [description, setDescription] = useState('');
	function handleSubmit(e) {
		e.preventDefault();
		console.log('Form submitted');
	}
	return (
		<form
			className='add-form'
			onSubmit={handleSubmit}
		>
			<h3>What do you need for your 😍 trip?</h3>
			<select>
				{Array.from({ length: 10 }, (_, i) => i + 1).map((num) => (
					<option
						value={num}
						key={num}
					>
						{num}
					</option>
				))}
			</select>
			<input
				type={'text'}
				placeholder='Item...'
				value={description}
				onChange={(e) => setDescription(e.target.value)}
			/>
			<button type={'submit'}>Add</button>
		</form>
	);
}
```

## State vs Props

                 State                                                                            Props

    1. Internal data, owned by component                                           1. External data, owned by parent component
    2. Component memory                                                            2. similar to function parameters
    3. Can be updated by the component itself                                      3. immutable
    4. Updating state causes component to re-render                                4. Receiving new props causes component to re-render
                                                                                      Usually when parents state has been updated
    5. Used to make components interactive                                         5. Used by parent to configure child components
