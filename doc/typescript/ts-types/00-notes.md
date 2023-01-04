# Notes

### Non-null Assertion Operator

- Just like other type assertions, this doesn’t change the runtime behavior of your code, so it’s important to only use `!` when you know that the value can’t be null or undefined.

```ts
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```

### null

- `typeof null` is actually "object"

### Falsy Values

- Falsy values in JS/TS
  - 0
  - NaN
  - "" (the empty string)
  - 0n (the bigint version of zero)
  - null
  - undefined

### Narrowing

- `typeof` type guards
- Truthiness
- Equality
- `in` operator
  - An operator for determining if an object has a property with a name
- `instanceof` narowing
  - An operator for checking whether or not a value is an “instance” of another value.
- [Assignments](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#assignments)
- [Control flow analysis](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#control-flow-analysis)
- [Using type predicates](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates)
- [Discriminated Unions](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions)

  ```ts
  interface Shape {
    kind: 'circle' | 'square';
    radius?: number;
    sideLength?: number;
  }
  ```

  vs

  ```ts
  interface Circle {
    kind: 'circle';
    radius: number;
  }

  interface Square {
    kind: 'square';
    sideLength: number;
  }

  type Shape = Circle | Square;
  ```

- [Exhaustiveness Checking](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#exhaustiveness-checking)
