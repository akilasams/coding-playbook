# Structural Type System

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
