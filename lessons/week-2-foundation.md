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

## Muy Important Topics

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

| .NET LINQ  | JS Array |
| ---------- | -------- |
| Select     | Map      |
| SelectMany | FlatMap  |
| Where      | Filter   |
| Any        | Some     |
| All        | Every    |
| First      | Find     |

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

```typescript
const myAsyncFunction = async (): void => {
  await callSomething();
};
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

### State

Definition: Any non-static variable.

1. User is logged on or off.
2. Input is valid or invalid.
3. Current value of an input.
4. A button is disabled depending on our input validity.

![log in state](https://imgs.search.brave.com/uDsOXClHYjHC_N6sb60JMqBsrVS3nt6vHfzUDAkKBgU/rs:fit:1135:656:1/g:ce/aHR0cHM6Ly9jc3Mt/dHJpY2tzLmNvbS93/cC1jb250ZW50L3Vw/bG9hZHMvMjAxOC8w/Ny9zdGF0ZS1tYWNo/aW5lcy0yLnBuZw)

The hardest thing in React/Vue is **discovering** where your state needs to be. Because, state can only flow down!

### One-Way Data Flow

#### Data flow in both React and Vue goes one-way, down

#### Data flows down, callbacks flow up

![react data flow](https://imgs.search.brave.com/3EwocDlHOxmN1Theab6k54mTC8BgxikAEtfvglfYN3g/rs:fit:677:304:1/g:ce/aHR0cHM6Ly9taXJv/Lm1lZGl1bS5jb20v/bWF4LzExMDQvMSpS/cElpYTNTYUlLVnhh/YTJHN0NoOTBnLnBu/Zw)

```typescript
<First> // data can only be updated by passing a function to children
  <Second> // can only access parent data via props
    <Third> // can only update props data via function/callback
    </Third
  </Second>
</First>
```

Data down, functions up.

React doesn't support two way binding inside of components themselves, Vue does.

### Command

Question Time: Who knows what the command pattern is?

![question time](https://media.giphy.com/media/l0HlRnAWXxn0MhKLK/giphy.gif)

```csharp
public int GiveMeNumbers(int a, int b, int c) {
  // stuff
}

public int GiveMeNumbers(NumbersCommand command) {
  // stuff
}
```

```typescript
const MyComponent: React.FC<MyCommandProps> = ({ a, b, c, d, e }) => {
  return();
};

interface MyCommandProps {
  a: number;
  b: number;
  c: string;
  d: string;
  e: Date;
}
```

```typescript
interface MyCommand {
  a: number;
  b: number;
  c: string;
  d: string;
  e: Date
}

const MyComponent: React.FC<MyCommandProps> = ({ command }) => {
  return();
};

interface MyCommandProps {
  command: MyCommand;
}
```

**Personal Opinion:** Once you hit the 5-6 mark for parameters you are passing to any function, class, constructor, you should look to refactor that list.

**Hint:** Its going to be really annoying when you test that code to have to pass in all of those parameters!

### Separation of Concerns

React and Vue are not MVC, or MVVM, or MVP libraries. They are Component based.

Question Time: Who can define MVC/MVVM/MVP? Which of these is React or Vue?

![more questions](https://media.giphy.com/media/MZQkUm97KTI1gI8sUj/giphy.gif)

![the diff](https://imgs.search.brave.com/6iwqiHFR6n09iGBqboi9fbq4VZjswkG60xJ20HTg1zY/rs:fit:1024:504:1/g:ce/aHR0cHM6Ly93d3cu/c2ltZm9ybS5jb20v/d3AtY29udGVudC91/cGxvYWRzLzIwMTgv/MDEvTVZDLXZzLU1W/UC12cy1NVlZNLW1v/YmlsZS1hcHAtZGV2/ZWxvcG1lbnQucG5n)

Components are spaghetti, the good kind.

![spaghetti](https://media.giphy.com/media/11uoNyauChZR16/giphy.gif)

Good separation of concerns in components:

1. Keeping components pure (presentation only)
2. Keeping data access in special components (our form of DI)
3. Keeping styling in a manageable state (avoiding inline)
4. Moving complex logic to utility functions

Testing will force you to keep your separations in check!86

![react soc](https://reactjs.org/static/9381f09e609723a8bb6e4ba1a7713b46/90cbd/thinking-in-react-components.png)

### Composition

Question Time: Who can define composition? How is it different from aggregation?

![questions](https://media.giphy.com/media/XHVmD4RyXgSjd8aUMb/giphy-downsized-large.gif)

![comp vs agg](https://imgs.search.brave.com/osMPhTTWCTch5nDuOjTAFReRTllcLaYIQyQJlDEbVgo/rs:fit:514:181:1/g:ce/aHR0cHM6Ly9pLnN0/YWNrLmltZ3VyLmNv/bS9ZZU9yWi5qcGc)

```jsx
<Columns>
  <Column />
    <Column>{children}</Column> //content projection
  <Column />
</Columns>

<CenteredColumns>
  // content projection
</CenteredColumns>
```

#### Choking parameters

```jsx
const Button: React.FC<ButtonProps> = ({ options }) => {
  return (
    <button role="button" className={`button  ${options}`}>
      ClickMe
    </button>
  );
};

interface ButtonProps {
  options: string;
}
```

How would you do a large button?

```jsx
<Button options="is-large" />
```

or...

```jsx
const LargeButton: React.FC = () => {
  return <Button options="is-large" />;
};
```

#### Testing (Again)

There are two types of testing:

Normal functions: Just write a normal unit test

Components: Using testing library/user event/jest dom

![intermission](https://media.giphy.com/media/7z60uukpYWFLG/giphy.gif)

#### Homework

![hw](https://media.giphy.com/media/LNrYPitbb8D8A/giphy.gif)

1. Get your environment ready
2. Review any concepts you need to refresh your mind on
3. Read the React/Vue documentation a first time
4. (Optional) Make mistakes. Get messy. Write a component or two.
