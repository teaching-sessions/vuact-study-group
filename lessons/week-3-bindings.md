# Week 3: Bindings and Nodes and Projection (Oh my!)

## Goals

Understand the basics of how React and Vue approach building components, binding, and simple content projection.

## Key Learning Objectives

1. React JSX and Vue templates
2. How React and Vue approaching Binding
3. Content Projection

## Show And Tell

Who has a project that they would like to show the class?

![show and tell](https://media.giphy.com/media/g0EMaHVN5J2nOOaG6Y/giphy.gif)

## Backup Plan

![its treason then](https://media.giphy.com/media/n5Vd1YcBNA5eU/giphy.gif)

### Pop Quiz

1. How does data flow in React/Vue?
2. How does composition relate to React/Vue?
3. Is React JS first or HTML first? Vue?

## Vue templates

> Vue uses an HTML-based template syntax that allows you to declaratively bind the rendered DOM to the underlying component instance's data. All Vue templates are syntactically valid HTML that can be parsed by spec-compliant browsers and HTML parsers. - Vue Docs

Vue uses HTML compliant syntax to achieve its goals.

### Template

Template is an html tag that can hold content that will be loaded when needed.

```html
<template>
  <h2>Flower</h2>
  <img src="img_white_flower.jpg" />
</template>
```

How it looks inside a Vue component:

#### Component.vue

```html
<template>
  <h2>Flower</h2>
  <img src="img_white_flower.jpg" />
</template>

<script setup lang="ts">
  // TS goes in here
</script>
```

The setup tag is syntactic sugar in Vue for doing the following:

```javascript
import { defineComponent } from "vue";

export default defineComponent({
  name: "MyComponent",
  components: {},
  props: {},
  setup() {
    return {};
  },
});
```

.Vue files are just Vue's internal way of being able to combine both HTML and JS/TS, they serve the same function as JSX/TSX do in React.

The Volar and Volar (typescript) VSCode plugins allow you to get a decent level of intellisense from .Vue files.

The "reasoning" behind templates is that they enjoy "compile-time optimizations" that are not present in JSX/TSX.

#### Vue Bindings 101

##### Interpolation

Use the "mustache" for interpolation.

```html
<template>
  <p>{{ myDisplayText }}</p>
</template>

<script setup lang="ts">
  // omitted for brevity
</script>
```

##### Attributes

```html
<template>
  <p :class="has-text-primary">Hello There!</p>
</template>

<script setup lang="ts">
  // omitted for brevity
</script>
```

this is short for...

```html
<template>
  <p v-bind:class="has-text-primary">Hello There!</p>
</template>

<script setup lang="ts">
  // omitted for brevity
</script>
```

This is used for any major attribute such as class, id, disabled, role, aria-xxx, required, ect.

##### Expressions

Expressions can be done in either the "mustache" or ":" notation.

```html
<template>
  <p>{{ showText ? "Hello Michael" : "Sign In" }}</p>
</template>

<script setup lang="ts">
  import { defineProps } from "vue";

  defineProps<{
    showText: boolean;
  }>();
</script>
```

With expressions I have two logical branches. What does that mean?

![jack](https://media.giphy.com/media/ccRMvuh3PeuSGgOWVx/giphy.gif)

```typescript
describe("Basic Component", () => {
  it("Shows proper text when logged in", () => {
    render(BasicComponent, { props: { showText: true } });

    expect(screen.getByText(/hello michael/iu)).toBeInTheDocument();
  });

  it("Show proper text when logged out", () => {
    render(BasicComponent, { props: { showText: false } });

    expect(screen.getByText(/sign in/iu)).toBeInTheDocument();
  });
});
```

Expressions in attributes:

```html
<template>
  <p :class="isBlue ? 'is-blue' : 'is-red'">Hello There!</p>
</template>

<script setup lang="ts">
  import { defineProps } from "vue";

  defineProps<{
    isBlue: boolean;
  }>();
</script>

<style scoped>
  .is-blue {
    color: skyblue;
  }

  .is-red {
    color: maroon;
  }
</style>
```

and the test...

```typescript
describe("Class conditional", () => {
  it("Has correct class when blue", () => {
    render(ClassConditional, { props: { isBlue: true } });

    expect(screen.getByText(/hello there/iu)).toHaveClass("is-blue");
  });

  it("Has correct class when not blue", () => {
    render(ClassConditional, { props: { isBlue: false } });

    expect(screen.getByText(/hello there/iu)).toHaveClass("is-red");
  });
});
```

In Short:

Interpolation = {{ value }} = used between tags <>{{ junk }}<>
Attributes = :myAttribute="myVariable" = used inside of tags <:junk="moreJunk"></>

Directives will be covered in two weeks!
