# Week 4: Lists, Keys, Conditionals

## Goals

Understand how control flow and lists work in React and Vue alongside directives

## Key Learning Objectives

1. How React and Vue handle iterators
2. How to bind directives
3. How to handle control flow
4. Drawing Component Boundaries

### The Story about Storybook

> Storybook is an open source tool for building UI components and pages in isolation. It streamlines UI development, testing, and documentation.

![storybook](https://media.giphy.com/media/JTDFyCnKgVy4sRmKuz/giphy.gif)

Example Story:

```tsx
import type { ComponentMeta, ComponentStory } from "@storybook/react";
import Footer from "./Footer";
import bindJestTests from "../../common/test-utilities/BindJestTests";

const FooterStories: ComponentMeta<typeof Footer> = {
  component: Footer,
  title: "Layout/Footer",
};

export default FooterStories;

export const Template: ComponentStory<typeof Footer> = () => <Footer />;

bindJestTests("Footer.spec.tsx", Template);
```

What does storybook do for you?

| Team Member | Capabilities                                                                                                   |
| ----------- | -------------------------------------------------------------------------------------------------------------- |
| Developer   | Easy way to prototype new features, Document existing ones, lots of cools plugins for jest, a11y, mobile views |
| UX Dev      | See how your design looks in an isolated environment                                                           |
| PM/Owner    | Preview current dev status, smaller feedback loop                                                              |

You can [deploy your storybook](https://aca-dev-ohio-app.azurewebsites.net) to a cloud service just like a normal node app!

### Iterators

#### React

React and Vue have build in support for iterators when you need to loop through a 0-N collection.

React uses vanilla JS array functions:

```tsx
const MyComponent: React.FC = () => {
  const numbers = [1, 2, 3, 4, 5, 6];

  return (
    {numbers.map((num): JSX.Element => {
      return <p key={num}>{num}</p>
    })}
  )
};

export default MyComponent;
```

Make sure you return your statement! Its a very common mishap. If you enable the eslint [explicit function return](https://typescript-eslint.io/rules/explicit-function-return-type/) rule, you will not have this problem.

#### Vue

Vue has a build in directive for iterators, "v-for", it works exactly likes its angular counterpart!

```html
<template>
  <p v-for="num in numbers" :key="num">{{ num }}</p>
</template>

<script lang="ts">
  const numbers = [1, 2, 3, 4, 5, 6];
</script>
```

##### Keys

Both React and Vue need a way of keeping track of how many items are in a list. The key is an id value required for change tracking.

#### Iterating with Components

Iterating over basic and complex types is pretty standard, however, you can also iterate over components as well.

```tsx
const MyComponent: React.FC = () => {
  const numbers = [1, 2, 3, 4, 5, 6];

  return (
    {numbers.map((num): JSX.Element => {
      return <MyOtherComponent value={num} />;
    })}
  )
};

export default MyComponent;
```

```html
<template>
  <MyOtherComponent v-for="num in numbers" :key="num" value="num" />
</template>

<script lang="ts">
  const numbers = [1, 2, 3, 4, 5, 6];
</script>
```
