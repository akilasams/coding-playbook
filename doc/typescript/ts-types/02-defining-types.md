# Defining Types

- To create an object with an inferred type which includes `name: string` and `id: number`,

```ts
interface User {
  name: string;
  id: number;
}

const user: User = {
  name: 'Akila',
  id: 1,
};
// If you provide an object that doesn’t match the interface you have provided, TypeScript will warn you
```

- You can use an interface declaration with classes, to annotate parameters and return values to functions.
- It’s best not to add annotations when the type system would end up inferring the same type anyway.

## Type Aliases

Examples :

- Using the `type` keyword for defining custom types

```ts
//Type aliasing an object type
type Point = {
  x: number;
  y: number;
};

//Type aliasing an union type
type ID = number | string;
```

## Interfaces

- An interface declaration is another way to name an object type

```ts
interface Point {
  x: number;
  y: number;
}
```

- Type aliases and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an interface are available in type

## Interfaces and Types

- You’ll see that there are two syntaxes for building types
- You should prefer `interface`. Use `type` when you need specific features. Because you will get better, terser and more focused error messages
- They are very similar, and for the most common cases act the same.
- They both support extending other interfaces and types. Type aliases do this via intersection types, while interfaces have a keyword.

```ts
type Owl = { nocturnal: true } & BirdType;

interface Chicken extends BirdInterface {
  colourful: false;
  flies: false;
}
```

- the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable.

```ts
interface Kitten {
  purrs: boolean;
}

interface Kitten {
  colour: string;
}

// types get the duplicate identifier error if we try this
```
