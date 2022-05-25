# Week 1 Environment Setup & Structure

## Goals

To understand the basics of a Node front-end web application structure with respects to React and Vue.

> If you are new to React and Vue, I suggest you go with React.
>
> 1. Higher priority for Aspirent.
> 2. Higher adoption rate.
> 3. Easier to learn.

## Key Learning Objectives

1. Learn how to bootstrap a React or Vue project via their CLI's
2. Gain the basics of the application structure
3. Understand the supporting Node ecosystem and set of useful 3rd party libraries

## Overview

The great thing about the Node ecosystem is that React, Vue, and Angular share a common configuration pattern and set of supporting libraries!

> All examples will be shown in TypeScript. I am voluntelling everyone here nicely to please use TypeScript. It has so many upsides with functionally zero downsides.

## Things to know

### React "Philosophy"

1. JS/TS is a first-class citizen. You primarily write JS and add HTML into. (In comparison to Angular or Vue where you add JS to your HTML).
2. Write components in an abstraction called JSX.
3. Easy to learn, easy to shoot yourself in the foot.
4. React is a "View" library, not a framework.
5. One-way data flow and binding.

### Vue "Philosophy"

1. Uses template syntax similar to Angular with it's own .vue files.
2. Influenced by both React and Angular.
3. One-way data flow, but two-way binding.
4. Has "framework" aspects of a native router, state-management.

| Design | React | Vue | Angular
| ------ | ----- | --- | -------- |
| Syntax | JSX | Templates | Templates
| File Type | .jsx/.tsx | .vue | html/.ts
| Style | HTML in your JS | JS in your HTML | JS in your HTML
| Architecture | Component | Component | Hybrid MVVM-ish, Component
| Data-Flow | Uni-directional | Uni-directional | Uni-directional|
| Binding | One-Way | Two-Way | Two-way
| Framework? | No, Views Only | Yes, Plugins | Yes
| Local State | Hooks | Options or Composition API | Properties
| App State | State Store (Redux) | State Store (Pinia) | RxJs

> Nothing in the table above is a silver bullet or implies one is "better" than the other. You can write poor code in any library/framework.

## First Things First

1. Make sure you have NodeJS installed. Either 16.0 LTS or 18.0 CR will do.
2. NodeJS serves as a JavaScript runtime for React, Vue, Angular. Just like how .NET is the runtime for C#.
3. Have a recent version of Git installed your machine.
4. Install VSCode for your IDE/Editor. (It is highly recommended that you us VSCode as it is the de-facto editor for JS development.)

**Please refrain from being Functional Phil**
![No Vim/Emacs allowed](https://media.giphy.com/media/l0Iy1hI6DW90guoSY/giphy.gif)

## Bootstrapping a Project

### React

1. Open Git Bash
2. CD to the directory of your choosing

```bash
npx create-react-app my-app --template typescript
```

### Vue

1. Open Git Bash
2. CD to the directory of your choosing

```bash
npm install -g @vue/cli

vue create my-app
```

Suggested options:

![Vue Options](https://cli.vuejs.org/cli-select-features.png)

1. Babel (yes)
2. Typescript (yes)
3. PWA (optional)
4. Router (yes)
5. Vuex (yes)
6. CSS Pre-Processors (optional, if sass, use dart-sass)
7. Linter (yes, eslint + prettier)
8. Unit Testing (yes, jest)
9. E2E Testing (preferred, cypress)


