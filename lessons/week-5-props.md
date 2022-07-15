# Week5: Props and Containers

## Goals

Understand how to effectively work with props.

## Key Learning Objectives

1. How React and Vue handle properties
2. The different ways of using properties
3. Solving common issues
4. Solving dependencies with Containers

## Big Takeaway for Week 5

Props are easy, but have a number of tradeoffs you need to balance.

![two buttons](https://imgflip.com/s/meme/Two-Buttons.jpg)

Those tradeoffs are:

1. Where you draw your component boxes determine your props
2. Balancing the number of props with the needs of your components
3. How to condense props when needed

## How to Props

### Some Quick Rules

1. Props should be of the following:
    i. value types
    ii. functions
    iii. interfaces
2. They **can't** be generics (Blazor is the exception)
3. Props should be the defacto way of communicating between components

### The Golden Rules

![gold](https://media.giphy.com/media/wb6xgCSpLl0m4/giphy.gif)

1. Components are just functions
2. Props are just parameters
3. Any issues with components props can be solved the same way you solve issues with functions & parameters.
4. The over-under for max number of props is ~5.

#### Vue Emits

Vue has a feature called "emits" which are a way of raising a custom event in a component. These are bad for so many reasons:

```html
<button @click="$emit('ewwString', myData)">Gross</button>
```

1. Emits are an optional contract/nullable event (i.e. A component may raise an event but a parent may not listen)
2. Emits go around props, which is not how to handle component to component interaction
3. Why choose Vue if you are going to use raw events?
4. Defined with strings (easy to misspell/error prone)
5. Not inheritably type safe
6. If you find yourself wanting to use emits, your components probably need a redo
7. Hard to test, a normal callback function can be mock, can't do that with a hard-coded emit

### React Props

```tsx
interface MyComponentProps {
  value: number;
  updateValue(value: number) => void;
}
```

Inside a component...

```tsx
const MyComponent: React.FC<MyComponentProps> = ({ value, updateValue }) => {

  // use props in here

  return();
}

interface MyComponentProps {
  value: number;
  updateValue(value: number) => void;
}
```

### Vue Props

```typescript
<template>
  // html
</template>

<script lang="ts">
interface MyComponentProps {
  value: number;
  updateValue(value: number) => void;
}

defineProps<MyComponentProps>();
</script>
```

or inline...

```typescript
<template>
  // html
</template>

<script lang="ts">
defineProps<{
  value: number;
  updateValue(value: number) => void;
}>();
</script>
```

## Common Property issues

### Too Many Props

Our component is unwieldy because we are passing too many props:

```tsx
const MyComponent: React.FC<MyComponentProps> = ({ first, second, third, fourth, fifth }) => {
  return ();
}

interface MyComponentProps {
  first: number;
  second: string;
  third: boolean;
  fourth: (first: number) => void;
  fifth: (second: string) => void;
}
```

#### Extra Component

Extra new component:

Pros:

- Enforces good interface segregation

Cons:

- You can have too many components
- Not always available (some components follow a strict hierarchy)

```tsx
const SubComponent: React.FC<SubComponentProps> = ({second, fifth}) => {
  return();
}

interface SubComponentProps {
  second: string;
  fifth: (second: string) => void;
}
```

```tsx
const MyComponent: React.FC<MyComponentProps> = ({ first, second, third, fourth, fifth }) => {
  return ();
}

interface MyComponentProps {
  first: number;
  third: boolean;
  fourth: (first: number) => void;
}
```

```tsx
const Parent: React.FC = () => {
  return(
    <>
      <SubComponent second={second} fifth={fifth} />
      <MyComponent first={first} third={third} fourth={fourth} />
    </>
  )
};
```

#### Try To Apply Optional Parameters

Pros:

- easy

Cons:

- Optional parameters may indicate something should not be a prop

```tsx
const MyComponent: React.FC<MyComponentProps> = ({
  first = ValueDefault.Number,
  second = "MyDefaultValue",
  third,
  fourth,
  fifth
  }) => {
  return ();
}

interface MyComponentProps {
  first?: number;
  second?: string;
  third: boolean;
  fourth: (first: number) => void;
  fifth: (second: string) => void;
}
```

#### Consolidate Common Parameters

Pros:

- Allows you to extra common functionality
- Very good way to deal with form inputs

Cons:

- Easy to over abstract props
- May lead to type bloat

```typescript
interface IMyCommonInterface {
  first: number;
  fourth: (first: number) => void;
}

interface IMyOtherCommonInterface {
  second: string;
  fifth: (second: string) => void;
}
```

```tsx
const MyComponent: React.FC<MyComponentProps> = ({ first, second, third }) => {
  return ();
};

interface MyComponentProps {
  first: IMyCommonInterface
  second: IMyOtherCommonInterface;
  third: boolean;
}
```

#### Use The Command Pattern

Pros:

- Consolidate props easily
- Great if you have to drill props through multiple components

Cons:

- Can just kick the can down the road

```tsx
interface IMyCommand {
  first: number;
  second: string;
  third: boolean;
  fourth: (first: number) => void;
  fifth: (second: string) => void;
}
```

```tsx
const MyComponent: React.FC<MyComponentProps> = ({ command }) => {
  return ();
}

interface MyComponentProps {
  command: IMyCommand
}
```

#### Use Local State/Resolvers

- We will cover this in a future meeting.
- Reducers are just switch statements.

Pros:

- Can consolidate state via command Pattern
- Can reduce callbacks my dispatching actions instead

Cons:

- Work best for same types
- Can be overkill

```tsx
interface ILocalState {
  first: number;
  second: string;
  third: boolean;
}

enum Actions {
  fourth = 0,
  fifth = 1,
}
```

```tsx
const MyComponent: React.FC<MyComponentProps> = ({ state, reducer }) => {
  return ();
}

interface MyComponentProps {
  state: ILocalState;
  dispatcher: (action: Actions, value: string) => void;
}
```

### Drilling Props

Some component trees have lots of complexity:

A -> B -> C -> D -> E

State in component A is required in E, but has to go through B, C, and D

The same issues as too many props applies to this situation. You may also:

1. Be drawing your boxes suboptimal (Do you need a 5 deep tree when a 4 can do?)
2. Your UI is too complex (Work with your UI designer)

![le bagette](https://lucidar.me/en/web-dev-class/files/html-form-example.png)

![task based ui](https://www.lifewire.com/thmb/IsEAnrGEgByz0tHW7gcIttkczAA=/699x524/smart/filters:no_upscale()/control-panel-applets-5a46623113f129003723917b.PNG)

> Something you just have to drill props and their is nothing you can do about it.

![let it be](https://preview.redd.it/cg89ani7yr121.jpg?auto=webp&s=673c38f9bd0091a0d20b1f8f09438d51222ce559)

### Bad Prop types

There are certain props you **should not** pass.

1. style
2. className
3. ...or anything related to css.

[Good Read About Proper Prop Types](https://medium.com/@JanPaul123/don-t-pass-css-classes-between-components-e9f7ab192785) <- Because reasons

What is bad about the following?

```tsx
const Button: React.FC<ButtonProps> = ({ className, text, handleOnClick }) => {
  return (
    <button className={`button ${className}` onClick={handleOnClick}}>{text}</button>
    );

    interface ButtonProps {
      className?: string;
      text: string;
      handleOnClick(event: React.MouseEvent<HTMLButtonElement>) => void;
    }
}
```

This is akin to a public setter:

```csharp
public Guid Id { get; set; }
```

...better

```tsx
enum Color {
  Primary = 0,
  Secondary = 1,
}

const determineColor = (color: Color): void => {
  switch(color) {
    // blah blah blah
  };
}

const Button: React.FC<ButtonProps> = ({ className, text, color, handleOnClick }) => {
  return (
    <button className={`button ${determineColor(color)}` onClick={handleOnClick}}>{text}</button>
    );

    interface ButtonProps {
      color?: Color = Color.Primary,
      text: string;
      handleOnClick(event: React.MouseEvent<HTMLButtonElement>) => void;
    }
}
```

Components should not leak details and only provide explicit interfaces that conclude with a pre-defined state.

When you allow clients to pass anything, you open up the possibility of putting a component into an undefined state.

## Containers

What is so bad about the following?

```tsx
const MyComponent: React.FC = () => {
  const myDate = fetch('someApi.com');

  return ();
}
```

You can't test/mock the api call. We need a way to separate our concerns in React/Vue.

```tsx
describe('MyComponent', () => {
  it('does the thing', () => {
    render(<MyComponent />);

    // oh crap, calls production api, bad for post/put/deletes
  })
});
```

React/Vue don't have Services like Angular, you need to write your own.

...use a Containers

```tsx
const MyComponentContainer: React.FC = () => {
  const data = fetch('someApi.com');

  return (<MyComponent data={data} />);
}
```

```tsx
const MyComponent: React.FC<MyComponentProps> = ({ data }) => {
  // use data

  return ();
}

interface MyComponentProps {
  data: Array<string>;
}
```

...now its EZ Clap to test.

```tsx
describe('MyComponent', () => {
  it('does the thing', () => {
    const data = [];

    render(<MyComponent data={data} />);

    // assert whatever you want
  })
});
```
