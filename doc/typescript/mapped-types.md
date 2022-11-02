# TypeScript : Types

## Mapped Types

- Keywords like `Readonly<...>` are called mapped types.

````
type Todo = {
  readonly id: number
  readonly text: string
  readonly done: boolean
}
```js

- Mapped types are kind of like functions, except the input/output are TypeScript types.
- There are many built-in mapped types (like `Required<...>`, `Partial<...>` etc). You can also create your own mapped types.

## Intersection Types

## Union Types
````
