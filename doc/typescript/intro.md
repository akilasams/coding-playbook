# Intro

## About

- Language which builds on JavaScript
- TypeScript code is transformed to JS trough a compiler (e.g. TS Compiler, Babel)
- 2 Main pros
  - Type checking errors -> catch errors before they occur in production
  - Providing better documentation -> makes it much easier for you and others to understand code

## TS Compiler

- `tsc`, the typescript complier`npm install -g typescript`
- Lets take a look at the function below

```ts
function greet(person: string, date: Date) {
  console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}

greet('Maddison', new Date());
```

Let’s take a look at what happens when we compile the above function `greet` with `tsc` to output JavaScript

```js
'use strict';
function greet(person, date) {
  console.log(
    'Hello '.concat(person, ', today is ').concat(date.toDateString(), '!')
  );
}
greet('Maddison', new Date());
```

- Notice two things here
  - Our person and date parameters no longer have type annotations. (Erased Types)
    - TS compiler strip out or transform any TypeScript-specific code so that you can run it on browsers/other runtimes
  - Our “template string” - that string that used backticks (the ` character) - was converted to plain strings with concatenations. (Downleveling)
    - Template strings are a feature from a version of ECMAScript called ECMAScript 2015
    - By default TypeScript targets ES3
    - Running `tsc --target es2015 hello.ts` gives us the following output:
    ```js
    function greet(person, date) {
      console.log(`Hello ${person}, today is ${date.toDateString()}!`);
    }
    greet('Maddison', new Date());
    ```
