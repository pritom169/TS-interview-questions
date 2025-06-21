## What is the difference between JS and TS?

JS is natively executed inside the browser. That means any other language can not be executed.
The TS code needs to be transpiled into JS code, and only then it cane be executed inside the brower.

TS is not a seperate language. It has been built on top of Javascript. All the features of JS like
variables, arrays, classes, functions, all this stuff exists in TS.

When developing an application it, we have to run the application and if there are any errors, we would
have got it in runtime. Because TS provides type safety, we can catch the error much faster and we can
get the error in compiling time.

## Does TS improve our code out of the box?

Not exactly. We need to enable strict compiler options (strict: true).

## How to define basic types inside typescript?

### Variables

```ts
let name: string = "John";
let age: number = 25;
let isActive: boolean = true,
let data: any = "anything"
```

### Arrays

```ts
let numbers: [] = [1, 2, 3];
let names: Array<string> = ["Alice", "Bob"];
let mixed: (string | number)[] = ["text", 42];
```

### Functions

```ts
function greet(name: string): string {
  return `Hello, ${name}`;
}

const add = (a: number, b: number) => a + b;

function welcome(name: string, age?: number): void {
  console.log(`Welcome ${name}`);
}
```

### Objects

```ts
let user: { name: string; age: number } = {
  name: "John",
  age: 30,
};

interface User {
  name: string;
  age: number;
}

let person: User = { name: "Jane", age: 25 };
```

### Special Types

```ts
let nothing: null = null;
let notDefined: undefined = undefined;
let anything: any = "flexible";
let unknown: unknown = "safer than any";
```
