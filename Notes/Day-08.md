# Thinking in React (Components, Composition, Reusability)

## Component size matters

A component should neither be huge nor be small. Having a huge component have its disadvantages like might need too many props, will be hard to reuse, complex code and hard to understand. Similarly having a very small component also comes with its own disadvantages like we might end up with 100s of mini-components, confusing code-base, too abstracted (abstraction---> creating something new to hide the implementation details of that thing).

The goal here is that we need to find the right balance between too specific and too broad.

## How to split a UI into components

The 3 criteris for splitting a UI into components

- Logical separation
- some are re-usable
- Low complexity

### Framework: When to create a new component?

When in doubt start with a relatively big component, then split it into smaller components as it becomes necessary.

- Does the component contains pieces of content or layout that don't belong together?
- Is it possible to reuse part of the component? Do you want/need to reuse it?
- Is the component doing too many different things?
- Does the component rely on too may props?
- Does the component have too many pieces of state and/or effects ?
- Is the code, including JSX, too complex/confusing?

If all or any of there questions check then you need to create a new component

### Pre-Cautions

- Be aware that creating a new component creates a new abstraction. Abstrations have a cost, because more abstractions require more mental energy to switch back and forth between components. So try not to create new components too early
- Name a components according to what it does or what it displays. Don't be afraid of using long component names.
- Never declare a new component inside another component!
- Co-locate related components inside the same file. Son't separate components into different files too early.
