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

```tsx
const MyComponent: React.FC<MyComponentProps> = () => {
  return ();
}

```


## Containers


