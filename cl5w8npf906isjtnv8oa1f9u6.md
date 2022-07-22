## Typescript - Tips & Tricks - Literal Types

Welcome back!
Today I show you the [Literal Types](https://www.typescriptlang.org/docs/handbook/literal-types.html).

This feature permits you to create a set of relationship values.
```ts
type Direction = "North" | "South" | "East" | "West";
```
Literal types in this case create also a Type Guard of your field, so the compiler can detect your errors or your typos.
```ts
let directionError: Direction = "east" // Type '"east"' is not assignable to type 'Direction'
let direction: Direction = "East" // OK
```
You can create Literal Types from different types such as booleans, numbers, and strings, and you can combine together different types too.
```ts
type Valid = false | 0 | true | 1;
```

That's all for today
See you soon guys!