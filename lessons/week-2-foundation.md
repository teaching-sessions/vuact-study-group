# Week 2 Foundational Concepts

## Goals

To cover key topics that will serve as a foundation to all skills required to be proficient in font-end frameworks.

## Overview

It's all just HTML, CSS, and JavaScript at the end of the day.

EZ Clap right?

![EZ Clap](https://media.giphy.com/media/Rl9Yqavfj2Ula/giphy.gif)

## Commonly Referenced Websites

[W3 Schools](https://www.w3schools.com/)
[Mozilla Dev](https://developer.mozilla.org/en-US/)
[CSS Tricks](https://css-tricks.com/)
[React Docs](https://reactjs.org/docs/getting-started.html)
[Vue Docs](https://vuejs.org/guide/introduction.html)

## Topics

### HTML

I suggest you brush up on the HTML 5 semantic tags and input types.

[HTML 5 Quick Reference](https://html.com/html5/)

![HTML 5 Elements](https://www.w3schools.com/html/img_sem_elements.gif)

[HTML 5 Input Types](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types)

1. email
2. date
3. time
4. color
5. more....

Please don't "learn" html in depth, your browser, accessibility tools, linter will yell at you about most issues.

### CSS & SASS

[CSS Box Model](https://www.w3schools.com/css/css_boxmodel.asp)
[Basic Selectors](https://www.w3schools.com/css/css_selectors.asp)
[FlexBox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
[Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
[Sass Primer](https://sass-lang.com/guide)

Learn your browser dev tools! Half of fixing all css issues is being well versed with the dev tools in Chrome/Firefox.

[Firefox CSS Tools](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/examine_and_edit_css/index.html)

### JavaScript & Typescript

![JavaScript](https://imgs.search.brave.com/kiJqa3qHFuUh8o80xRFJRBzMnhF1N3qY-E8NOWYqvGs/rs:fit:1200:1200:1/g:ce/aHR0cHM6Ly9pLnJl/ZGQuaXQvaDdudDRr/ZXlkN295LmpwZw)

[ES5](https://www.w3schools.com/js/js_es5.asp)
[ES6](https://www.w3schools.com/js/js_es6.asp)
[TypeScript Basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html)

> React and Vue are very functional. Get "gud" with functions and functional programming.

#### Arrow Functions

Super basic arrow function:

```typescript
const MyFunction = (): number => return 1;
```

React Component:

```typescript
const MyComponent: React.FC = () => {
  return <div>Hi There!</div>;
};

export default MyComponent;
```

even Components have arrow functions....

```typescript
const MyComponent: React.FC = () => {

  const MyFunction = (): void => return;

  return <div>Hi There!</div>;
};

export default MyComponent;
```

then we'll even pass functions to our functions...

```typescript
const MyComponent: React.FC<MyProps> = ({ func }) => {
  const MyFunction = (): void => {
    func();
  };

  return <div>Hi There!</div>;
};

interface MyProps {
  func: () => void;
}

export default MyComponent;
```

...finally, we'll write a function that wraps other functions that will be passed to our function.

![Inception](https://media.giphy.com/media/7pHTiZYbAoq40/giphy.gif)

```typescript
const MyHook = (): IHook => {
  const [get, set] = useState<number>(0);

  return [
    get,
    set,
  ];
};

const MyComponent: React.FC<MyProps> = ({ hook }) => {
  const MyFunction = (): void => {
    const state = func[0];
  };

  return <div>Hi There!</div>;
};

interface MyProps {
  hook: IHook;
}

export default MyComponent;
```

![Kronk](https://media.giphy.com/media/KEYEpIngcmXlHetDqz/giphy.gif)

The point is, React and Vue use functions...

#### Callbacks


