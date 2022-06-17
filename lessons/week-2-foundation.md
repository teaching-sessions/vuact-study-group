# Week 2: Electric Boogaloo (Foundational Concepts)

## Goals

To cover key topics that will serve as a foundation to all skills required to be proficient in font-end frameworks.

## Key Learning Objectives

1. Understand what concepts yield us the best bang for our buck
2. Cover key JS/TS topics that will be required for React and Vue
3. Discuss reoccurring patterns that present themselves in component based frameworks

## Show and Tell

Who would like to present their week 1 solution to the class?

![show me](https://media.giphy.com/media/3orifdyb5uQljmxgeA/giphy.gif)

## Overview

It's all just HTML, CSS, and JavaScript at the end of the day.

Remember the build folder I showed from the previous week?

EZ Clap right?

![EZ Clap](https://media.giphy.com/media/Rl9Yqavfj2Ula/giphy.gif)

## Commonly Referenced Websites

[W3 Schools](https://www.w3schools.com/)
[Mozilla Dev](https://developer.mozilla.org/en-US/)
[CSS Tricks](https://css-tricks.com/)
[React Docs](https://reactjs.org/docs/getting-started.html)
[Vue Docs](https://vuejs.org/guide/introduction.html)

## Muy Importante Topics

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

#### ES5 (2009)

##### Array methods of the young and restless

| .NET Linq  | JS Array |
| ---------- | -------- |
| Select     | Map      |
| SelectMany | FlatMap  |
| Where      | Filter   |
| Any        | Some     |
| All        | Every    |
| Find       | First    |

[Underscore.js](https://github.com/jashkenas/underscore) - More utility functions.

##### Strict Mode

Enabled by default in your tsconfig.ts, please keep on.

Covers 8 possible compile issues.

#### ES6 (2015)

Use let and const for variables.

[ESLint rule](https://eslint.org/docs/rules/no-var) - Not enabled in recommended rule-set or react template.

##### Arrow Functions

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

  return [get, set];
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

![Use the lever](https://media.giphy.com/media/KEYEpIngcmXlHetDqz/giphy.gif)

The point is, React and Vue use functions...

##### For/of

```typescript
for (let num of numbers) {
  console.log(num);
}
```

##### Callbacks

Simple: Passing a function as an argument.

```typescript
const Print = (msg: string): void => {
  console.log(msg);
};

const DoSomething = (printer: (msg: string) => void): void => {
  if (error) {
    printer(error);
  } else {
    // something else.
  }
};
```

**Callbacks are just like ordering pizza!**

![Krusty Krab](https://media.giphy.com/media/5hfYHLgvhBaKI/giphy.gif)

Do you just wait at the front door or do something else until the door bell rings?

###### JavaScript then chains

```typescript
let widgets = [];

HttpClient.GetStuff().then((result) => (widgets = result));
```

###### Event Handling

```typescript
const submitForm = (event): void => {
  // send to API
}

<button type='submit' onClick={submitForm}>
```

###### Callbacks as Props

```typescript
const Form: React.FC<FormProps> = ({ submitForm }) => {
  return( /* lots of jsx */
  <button type='submit' onClick={submitForm}>);
}

interface FormProps {
  onSubmit: () => void;
}

export default Form;
```

##### Promises

Question Time: Who can define a ES6 Promise?

PS: Use .NET Task as your reference.

PPS: I am looking for one very specific word.

![question time](https://media.giphy.com/media/3o7buirYcmV5nSwIRW/giphy.gif)

###### Using Async Code

```typescript
class HttpClient {
  public static GetStuff(): Promise<WidgetResponse> {
    return new Promise((resolve, reject) => {
      if(nothingBadHappened) {
        resolve(new WidgetResponse());
      }
      reject(new Error());
    })
  }
}

let widgets = [];

HttpClient.GetStuff().then((result) => (widgets = result));

or...

const widgets = await HttpClient.GetStuff();
```

[ESLint plugin for promises](https://github.com/xjamundx/eslint-plugin-promise) - Lots of nice rules for ES6 promises.

If you already know how Tasks/async/await work in .NET, you're 90% of the way there.

##### Destructuring Arrays and Objects

###### Arrays

React hooks use lots of array destructuring.

```typescript
const [a, b] = [1, 2];

a++;
b = a + b;
```

...using React hooks.

```typescript
const [count, setCount] = useState<number>(0);

console.log(count);
setCount(19);
```

...without destructuring.

```typescript
const countState = useState<number>(0);

console.log(countState[0]);
countState[1](19);
```

###### Objects

Used when passing props to a component.

```typescript
const myObj = {
  count: number;
  setCount: (value: number) => void;
};

let count = myObj.count;
let setCount = mjObj.setCount;

const { count, setCount } = myObj;
```

...using in a component props.

```typescript
const MyComponent: React.FC<MyComponentProps> = ({ count, setCount }) => {
  console.log(count);
  setCount(19);

  return (/* our jsx */);
}

interface MyComponentProps {
  count: number;
  setCount: (value: number) => void;
}

export default MyComponent;
```

##### Spread operator

```typescript
const myObj = {
  count: number;
  setCount: (value: number) => void;
};

function someFunc(count: number, setCount: (value: number) => void): void {
  // do something
}

someFunc(...myObj);

const myArray = [2, 3, 4];

const spreadArray = [...myArray];

```

**Personal opinion**: Avoid the spread operator in typescript when possible. Biggest exception is when you need to clone an object/array to update state.

[structured clone](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone) - Alternative that isn't quite supported in the CRA yet, waiting on Jest 28.

[React no spread props](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-props-no-spreading.md) - Not enabled by default.

**More to come later!**
