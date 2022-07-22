## Typescript - Tips & Tricks - readonly modifier

How many times we expect an object property to have a value but it isn't?
![Magic gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1658481317732/6z2RH04Gg.gif)
In these cases, unfortunately, we spend a lot of time searching for who changes the value of this property.
Today I want to show you a special modifier that helps you to prevent this problem and preserve your time.
This modifier is the [readonly](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#readonly-and-const).
The readonly modifier helps you to prevent someone can change your property, so, the object's property can set only in the object initialization.
A simple example
```ts
type Point = {
  x: number;
  y: number;
};
const point: Point = {
  x: 10,
  y: 10,
};
point.x = 20;
point.y = 20;

type ReadOnlyPoint = {
  readonly x: number;
  readonly y: number;
};
const readOnlyPoint: ReadOnlyPoint = {
  x: 10,
  y: 10,
};
readOnlyPoint.x = 20; // Cannot assign to 'x' because it is a read-only property
readOnlyPoint.y = 20; // Cannot assign to 'y' because it is a read-only property
```
In this example you can see how in the first case you can change the value of the properties 'x' and 'y'; on the contrary, in the second case, you can't change the properties because they are marked as readonly.
As you can see, the readonly modifier can prevent the change of the values of the properties and save your code from annoying bugs.
Typescript also exposes a special type to convert your types to full readonly types; this type is called _ReadOnly_.
So we can review the previous example in this way
```ts
type Point = {
  x: number;
  y: number;
};
const point: Point = {
  x: 10,
  y: 10,
};
point.x = 10;
const readOnlyPoint: ReadOnly<Point> = {
  x: 10,
  y: 10,
};
readOnlyPoint.x = 10; // Cannot assign to 'x' because it is a read-only property
readOnlyPoint.y = 20; // Cannot assign to 'y' because it is a read-only property
```

From the readonly modifier, it's all!
Goodbye guys!