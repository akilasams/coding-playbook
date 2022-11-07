# TypeScript : Types

## The Primitives

- In JS
  - `string`, `number`, `bigint`, `boolean`, `null`, `symbol`, `undefined`
- TS extends this list with a few more.
  - `any` - allow anything
  - `unknown` - ensure someone using this type declares what the type is
  - `never` - it’s not possible that this type could happen
  - `void` - a function which returns `undefined` or has no return value
- To learn the type of a variable, use `typeof`

## Defining Types

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

### Optional Properties

```ts
function printName(obj: { first: string; last?: string }) {
  // ...
}
// Both OK
printName({ first: 'Bob' });
printName({ first: 'Alice', last: 'Alisson' });
```

- In JS, if you access a property that doesn’t exist, you’ll get the value `undefined` rather than a runtime error. Because of this, when you read from an optional property, you’ll have to check for `undefined` before using it.

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

- One major difference between type aliases vs interfaces are that interfaces are open and type aliases are closed. This means you can extend an interface by declaring it a second time. A type cannot be changed outside of its declaration.

```ts
interface Kitten {
  purrs: boolean;
}

interface Kitten {
  colour: string;
}

// types get the duplicate identifier error if we try this
```

## Composing Types

With TypeScript, you can create complex types by combining simple ones. There are two popular ways to do so,

- unions
- generics

#### Unions

- A popular use-case for union types is to describe the set of string or number literals that a value is allowed to be.
  - `type WindowStates = "open" | "closed" | "minimized";`
- Unions provide a way to handle different types too. you may have a function that takes an array or a string
  - `function getLength(obj: string | string[]) { return obj.length; }`

#### Generics

- Generics provide variables to types.
- A common example is an array. An array without generics could contain anything. An array with generics can describe the values that the array contains.

```ts
type StringArray = Array<string>;
type NumberArray = Array<number>;
type ObjectWithNameArray = Array<{ name: string }>;
```

- You can declare your own types that use generics

```ts
interface Backpack<Type> {
  add: (obj: Type) => void;
  get: () => Type;
}

//This line is a shortcut to tell TypeScript there is a constant called `backpack`, and to not worry about where it came from
declare const backpack: Backpack<string>;

// object is a string, because we declared it above as the variable part of Backpack.
const object = backpack.get();

// Since the backpack variable is a string, you can't pass a number to the add function.
backpack.add(23); // Argument of type 'number' is not assignable to parameter of type 'string'.
```

## Structural Type System

- The point variable is never declared to be a Point type. However, TypeScript compares the shape of point to the shape of Point in the type-check. They have the same shape, so the code passes. The shape-matching only requires a subset of the object’s fields to match

```ts
interface Point {
  x: number;
  y: number;
}

function logPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}

// logs "12, 26"
const point = { x: 12, y: 26 };
logPoint(point);

const point3 = { x: 12, y: 26, z: 89 };
logPoint(point3); // logs "12, 26"

const color = { hex: '#187ABF' };
logPoint(color); // error : Type '{ hex: string; }' is missing the following properties from type 'Point': x, y
```

- There is no difference between how classes and objects conform to shapes, the object or class has all the required properties, TypeScript will say they match, regardless of the implementation details.

## Intersection Types

## Union Types

```ts
function printId(id: number | string) {
  console.log('Your ID is: ' + id);
}
// OK
printId(101);
// OK
printId('202');
```

## Mapped Types

- Keywords like `Readonly<...>` are called mapped types,

```ts
type Todo = {
  readonly id: number;
  readonly text: string;
  readonly done: boolean;
};
```

The above code is equivalent to the following version

```ts
type Todo = Readonly<{
  id: number;
  text: string;
  done: boolean;
}>;
```

- Mapped types are kind of like functions, except the input/output are TypeScript types.
- There are many built-in mapped types (like `Required<...>`, `Partial<...>` etc). You can also create your own mapped types.
