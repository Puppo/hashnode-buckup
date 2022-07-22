## Typescript - Tips & Tricks - Non-null assertion operator

In some cases, you have a field that you initialize in a method, and if you follow the flow of the code you are sure that this field is initialized but typescript doesn't understand it.
An example
```ts
type Person = {
  name: string;
};

let person: Person;

function initialize() {
  person = { name: "name" };
}

initialize();
console.log("Hello", person.name); // Variable 'person' is used before being assigned.
```
In this case, you can see how the typescript compiler doesn't understand that the "person" field isn't null but it's initialized.
To resolve this problem, the typescript language exposes us the _"Non-null assertion operation"_(!). This operator says to the compiler that the field isn't null or undefined but it's defined.
The previous example can be reviewed in this way
```ts
type Person = {
  name: string;
};

let person: Person;

function initialize() {
  person = { name: "name" };
}

initialize();
console.log("Hello", person!.name);
```
As you can see, in this case, the code doesn't have errors and the compilation ends with success.

That's all for today!
Bye-bye guys!