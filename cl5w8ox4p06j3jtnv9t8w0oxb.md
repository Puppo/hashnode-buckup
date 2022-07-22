## Typescript - Tips & Tricks - keyof

Welcome back!
Today I'll talk about the **keyof** operator.

This operator helps us to extract the object's properties such as [Literal-types](https://dev.to/puppo/typescript-tips-tricks-literal-types-10md)
```ts
type Person = {
  firstName: string;
  surName: string;
  age: number;
  location: string;
};

type PersonKeys = keyof Person; // "firstName" | "surName" | "age" | "location"
```
This operator can help us to create new methods that should depend of other types; e.g.
```ts
function get<T, K extends keyof T>(obj: T, prop: K): T[K] {
  return obj[prop];
}

function set<T, K extends keyof T>(obj: T, prop: K, value: T[K]): void {
  obj[prop] = value;
}
```
but also to create new types from other types e.g
```ts
type ReadOnly<T> = {
  readonly [K in keyof T]: T[K];
};

type ReadOnlyPerson = ReadOnly<Person>
/*
type ReadOnlyPerson = {
    readonly firstName: string;
    readonly surName: string;
    readonly age: number;
    readonly location: string;
}
*/
```

How we can see this operator is more powerful and it can help us to create new strict type or new strict methods.

That's all for today.
See you soon guys!

