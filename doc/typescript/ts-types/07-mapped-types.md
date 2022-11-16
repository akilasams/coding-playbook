# Mapped Types

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
