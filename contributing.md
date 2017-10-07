# Contributing

If you are looking to help to with a code contribution our project uses Node (with ES6 features). If you don't feel ready to make a code contribution yet, no problem! A great place to start is making sure with any holes in [the documentation](https://github.com/sjones6/funcatron-docs) or adding to the examples.

Checkout the [current projects](https://github.com/sjones6/funcatron/projects) to see what features need developed or are in progress.

Funcatron uses functional programming in JS. Here are some helpful places to learn functional programming in JS:

* [Fun Fun Function (channel and linked playlist)](https://www.youtube.com/watch?v=BMUiFMZr7vk&list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84)
* [_Composing Software_ series by Eric Elliott](https://medium.com/javascript-scene/the-rise-and-fall-and-rise-of-functional-programming-composable-software-c2d91b424c8c#.2dfd6n6qe)

You'll also want to be familiar with ES6, especially arrow functions, rest and spread, and object destructuring. [Here's a good summary](https://github.com/lukehoban/es6features).

Generally speaking, here are some the ways that Funcatron uses functional programming by convention:

* Never use `new` or `this` if at all possible (use closures instead)
* Use `const` and _rarely_ `let` when it's necessary to declare variables
* ES6 arrow functions to succinctly create functions
* No side effects but `pipe` values through a sequence of functions
* Rarely modify parameters (the one exception is the `req`, `res`, and `opt` objects) but return a new value

## What does the [Code of Conduct](https://github.com/sjones6/funcatron/blob/master/CODE_OF_CONDUCT.md) mean for me?

Our [Code of Conduct](https://github.com/sjones6/funcatron/blob/master/CODE_OF_CONDUCT.md) means that you are responsible for treating everyone on the project with respect and courtesy regardless of their identity. If you are the victim of any inappropriate behavior or comments as described in our Code of Conduct, we are here for you and will do the best to ensure that the abuser is reprimanded appropriately, per our code.

## Developing Funcatron

To setup the environment, you will need ... 

* Clone the [repository](https://github.com/sjones6/funcatron)
* [Node](https://nodejs.org/en/) installed on your machine (verion 8 is preferable)

A couple developer tools are setup to make the work easier:

* Watch files for changes, run tests, and restart the example project: `node watcher.js` 
* run tests with mocha: `npm test`
* For VS Code users: there's a few launch scripts bundled in `.vscode` directory

## First Time contributing to Open Source?

Here's a [handy guide](/first-timers.md) to help get you started! And feel free to ask questions if you get stuck!