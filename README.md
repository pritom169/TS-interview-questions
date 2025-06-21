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

## Difference between explicit and implicit styles in TS

In explicit style, one manually declare types for varaibles, function parameters, return types, etc.

```ts
let name: string = "Alice";
function greet(user: string): string {
  return `Hello, ${user}`;
}
```

In implicit style, one relies TS's type inference to determine the types for you.

```ts
let name = "Alice";
function greet(user) {
  return `Hello, ${user}`;
}
```

## Type in TS

A `type` is a type-alias-a way to give a name to a specific type (primitive, union, intersection
tuple, etc.).

```ts
type User = {
  name: string;
  age: number;
};

type ID = string | number;
```

- Creating complex types using union, intersection, and tuples
- Representing primitive, object, or function types

## Interface in TS

An interface defines the structure of an object. It's more limited than type, but it's better suited for
object-oriented design and can be extended multiple times.

```ts
interface User {
  name: string;
  age: number;
}
```

## Difference between type and interface

- Declaration merging is possible with `interface`, however it is not possible with `type`
- `type` is used for complex types and utility types, whereas `interfaces` are good for Object oriented and
  class-based designs.

## Union Type

A union type is written using the pipe symbol (|)

```ts
let value: string | number;

value = "hello";
value = 42;
value = true: // Error, as value only expecting string or number
```

### Type narrowing in Union

Narrowing means refining a union type to a specific type at runtime using conditional checks.

```ts
function printId(id: string | number){
    if (typeof id === "string) {
        console.log("String ID: ", id.toUpperCase());
    } else {
        console.log("Numeric ID: ", )
    }
}
```

## Void

Void represents the absence of value (especially for functions that don't return anything)

```ts
function logMessage(message: string): void {
  console.log(message);
}
```

> One should not assign a `void` value to anything except `undefined`. You can not do much with `void``

## never

Represents a value that never occurs.

One should use never when

- A function never returns (e.g., throws an error or has an infinite loop)
- Used to catch exhaustiveness in switch statements

```ts
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {}
}
```

```ts
type Shape = { kind: "circle" } | { kind: "square" };

function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return 1;
    case "square":
      return 2;
    default:
      const _exhaustiveCheck: never = shape; // Type error if new type added
      return _exhaustiveCheck;
  }
}
```
