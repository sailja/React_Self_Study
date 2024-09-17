### Component Categories

Most of your component will naturally fall into one of three categories:

1. Stateless/presentational components
   - No state
   - Can recieve props and simply present recieved data or other content
   - Usuallu small and reusable
2. Stateful components
   - Have state
   - Can still be re-usable
3. Structural components
   - `pages`, `layouts`, or `screens` of the app
   - Resultof composition
   - Can be huge and non-reusable(but don't have to)

### Prop Drilling

Prop drilling means passing a prop through several nested child components in order to get it to some deeply nested component.
Basically if we pass a prop from main component to its child to its child and then again to its child and so on.

## Component Composition

It is the technique of combining different components using the children prop (or explicitly defined props)

We use component composition for the following reasons:

- create highly re-usable and flexible components.
- Fix prop drilling(great for layouts)

## Props as an API

When working on a project in a team there might me multiple people consuming the component created by you. We need to make sure that the component is flexible and not too much complex. We need to find the right balance between too little and too many props, that works for both the consumer and the creator based on the project needs.

Using too many props will make the component too hard to use, too much complex and will make hard to write code. On the other hand using too little props will make the component not flexible enough and also might not be useful. In case you need to use too maky props make sure that you define some default values for some of the props.
