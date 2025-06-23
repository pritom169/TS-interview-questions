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

## any

Any disables type checking for a variable. One can assign anything to it, and it can be asssigned to anything.

Any should be avoided if possible. It can be used only you are migrating from JS to TS and you can not find
a type yet.

```ts
let value: any = 5;
value = "hello";
value = { x: true };

value.doesNotExist();
```

> Any defeats the purpose of TS's safety. One needs to use `unknown` if safety with flexibility in needed.

## Unknown

`Unknown` is like `any`, but type-safe. One must `narrow` it before one can use it.

When dealing with external input (e.g. JSON, user input) and want type safety, then one can use unknown.

```ts
let value: unknown = "hello";

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
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

## DOM manipulation in TS

In TS you use the DOM just like JS, but TS gives you the type safety and intellisense.

```ts
const button = document.getElementById("myButton") as HTMLButtonElement;

button.addEventListener("click", () => {
  console.log("Button clicked!");
});
```

> We use type assertions like `as HTMLInputELement` for specific elements. TS knows the structure of
> HTML elements, hence it provides auto completion.

## Classes in TS

TS classes are similar to ES6 classes but with type annotation, access modifiers, and interfaces.

```ts
class Person {
  private name: string;
  public age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, my name is ${this.name}`;
  }
}

const user = new Person("Alice", 30);
console.log(user.greet());
```

### Key features of classes

- classes can have `public, private, and protected properties`
- classes implements interfaces
- it can use `readonly` and `static`

## Enums in TS

Enums are a way to define a set of named constants

### Numeric Enum

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

let move: Direction = Direction.up;
```

### String Enum

```ts
enum Status {
  Success = "SUCCESS",
  Error = "ERROR",
}

let result: Status = Status.Success;
```

### Use cases of enums

- When readable and safe constant values are needed
- You need a specific set of allowed options

## Generics in TS

Generic allow you to create `reusable, type-safe components or functions` that work with any data type.

### Generic Function

```ts
function identity<T>(value: T): T {
  return value;
}

let result = identity<number>(42); // Identitiy function will return an integer
let word = identity<string>("hello"); // Word function will return a string
```

### Generic Interface

```ts
interface ApiResponse<T> {
  data: T;
  success: boolean;
}

const response: ApiResponse<string> = {
  data: "User created",
  success: true,
};
```

> We use generic to increase the reusability of the code as it workd with multiple types. In adverently,
> it also provides type safety.

## Tuples in TS

A tuple is a `fixed length array` with `typed-elements`.

```ts
let person: [string, number] = ["Alice", 30];

const [name, age] = person;
```

> Tuples are useful in inforcing specific types at specific positions. It is also quite handy
> in returning multiple values.

## Optional Properties in TS

In TS you put one "?" mark after `property name` or `type alias`:

```ts
interface User {
  id: number;
  name: string;
  email?: string; // Optional property has been declard
}
```

Here, `email` may be present or undefined

```ts
const u1: User = { id: 1, name: "Alice", email: "alice@example.com" };
const u2: User = { id: 2, name: "Bob" };
```

### How does Optional works underneath

- At compile time, TS knows that `user.email` might be `undefined`.
- When it has be transpiled into JS we might find the JS code is `email: string | undefined`.

```ts
function greet(user: User) {
  console.log(`Hi, ${user.name}`);

  if (user.email) {
    console.log(`Email: ${user.email.toLowerCase()}`);
  }
}
```

## Dynamic keys (Index Signatures) in TS

When you do not know all the property names in advance, you can use an `index signatures` or utlity types.

```ts
interface StringMap {
  [key: string]: string;
}
```

In the above mentioned example, string key is allowed, and value must be a `string`.

```ts
interface Config {
  port: number;
  [key: string]: string | number;
}

const cfg: Config = { port: 8080, host: "localhost", mode: "dev" };
```

## RecordType in TS

Record is a utility type that creates an object type with specific key-value type constraints.

```ts
type Scores = Record<string, number>;
const gameScores: Scores = {
  player1: 100,
  player2: 85,
  player3: 92,
};

// Record with specific string literal keys
type Status = Record<"pending" | "approved" | "rejected", "boolean">;
const taskStatus: Status = {
  pending: true,
  approved: false,
  rejected: false,
};
```

> Record type enforces consisted value types accross all properties.

## Pick and Omit in TS

These utility types create new types by selecting or excluding properties from existing types.

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
  age: number;
}

type UserSummary = Pick<User, "id" | "name">;

const summary: UserSummary = {
  id: 1,
  name: "John",
};
```

Omit is complete opposite of Pick. When Omit is performed, a particular
property will be omitted.

```ts
// we need to omit password for public user
type publicUser = Omit<User, "password">;

const publicData: PublicUser = {
  id: 1,
  name: "John",
  email: "john@example.com",
  age: 30,
};
```

## Readonly in TS

These utility type make properties immutable to prevent accidental modifications.

```ts
interface User {
  id: number;
  name: string;
  settings: {
    theme: string;
    notifications: boolean;
  };
}

type ReadonlyUser = Readonly<User>;
// Because of these all top level properties become raedonly

const user: ReadonlyUser = {
  id: 1,
  name: "John",
  settings: { theme: "dark", notifications: true },
};

// user.id = 2;              // Error: Cannot assign to 'id'
// user.name = "Jane";       // Error: Cannot assign to 'name'
user.settings.theme = "light"; // Works! Nested objects not affected
```

## Partial in TS

Partial makes all properties of a type optional by adding ? to each property.

```ts
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}

type PartialUser = Partial<User>;
// Result: {
//     id?: number;
//     name?: string;
//     email?: string;
//     age?: number;
// }

const user: PartialUser = {
  name: "John",
  // Other properties are optional
};
```

Some real world use cases

```ts
function updateUser(id: number, updates: Partial<User>) {
  // Can update any subset of user properties
  return { ...existingUser, ...updates };
}

updateUser(1, { name: "Jane" }); // Only name
updateUser(1, { email: "new@email.com" }); // Only email
updateUser(1, { name: "Bob", age: 25 }); // Multiple properties
```

## Required in TS

Required makes all properties of a type mandatory by removing the ? optional modifier.

```ts
interface User {
  id?: number;
  name?: string;
  email?: string;
  age?: number;
}

type RequiredUser = Required<User>;
// Result: {
//     id: number;        // ? removed
//     name: string;      // ? removed
//     email: string;     // ? removed
//     age: number;       // ? removed
// }

const user: RequiredUser = {
  id: 1,
  name: "John",
  email: "john@example.com",
  age: 30,
  // All properties are now mandatory
};
```

Some real world use cases

```ts
interface UserInput {
  id?: number; // Optional for creation
  name?: string;
  email?: string;
  createdAt?: Date;
}

// After saving to database, all fields should exist
type SavedUser = Required<UserInput>;

function saveUser(input: UserInput): SavedUser {
  const savedUser: SavedUser = {
    id: generateId(),
    name: input.name || "Unknown",
    email: input.email || "",
    createdAt: new Date(),
  };
  return savedUser;
}
```

## Literal Types in TS

Literal types allow you to specifiy exact value that a variable can hold, not just the general type.

### String Literal Type

```ts
// Instead of accepting any string
let direction: string = "up"; // Can be any string

// We use literal types for specific values only
let movement: "up" | "down" | "left" | "right" = "up";
// movement = "diagonal"; // Error: not allowed

type Theme = "light" | "dark" | "auto";
let userTheme: Theme = "dark"; // Only these 3 values allowed
```

## Template Literal Types

```ts
type EventName = `on${string}`;
let event: EventName = "onClick"; // Valid
let event2: EventName = "onSubmit"; // Valid
// let event3: EventName = "click";   // Error: doesn't start with "on"

// More complex patterns
type CSSUnit = `${number}px` | `${number}%` | `${number}rem`;
let width: CSSUnit = "100px"; // Valid
let height: CSSUnit = "50%"; // Valid
// let size: CSSUnit = "large"; // Error: doesn't match pattern
```

## What does TS as a language consists of?

TS has three main components:

1. The TS language itself
2. The TS compiler
3. The TS language service

### 1. The TS language

The language consists of syntax, keywords, and type annotations.

### 2. The TS Compiler (TSC)

The TSC converts instructions written in TS to it JS equivalent

### 3. The TS language Service

An additional layer of editor-like applications, such as statement completion, signature help, code formatting,
and colorization, among other things.

## How to transpile TS to JS

The easiest way to transpilte TS to JS by using TypeScript command line tool. An example command has been added.

```zsh
./node_modules/typescript/bin/tsc src/main.ts --outfile build.js
```

- `src/main.ts` is the file I want to transpile
- `build.js`is the file where all the transpiled code will be stored

## d.ts file in TS

A `.d.ts` file in TypeScript is a declaration file. Its purpose is to describe the shape of JavaScript code to the TypeScript compiler — essentially acting as a type definition without containing any actual implementation.

### Purpose of .d.ts Files

- Provide type information for existing JS code (like libraries)
- Enable IDE support like IntelliSense, autocompletion, and type checking
- Allow integration with untyped or third-party JS libraries

```ts
function greet(name) {
  return `Hello, ${name}`;
}
```

One can create a `.d.ts`file to declare types for it:

```ts
declare function greet(name: string): string;
```

Now the TS knows about the greet function, even though it's implemented in plain JS.

## Function Overloading in TS

Function overloading allows you to define multiple type signatures for the same function,
enabling different parameter combinaitons while maintaining type safety.

```ts
// Overload signatures (declarations only)
function greet(name: string): string;
function greet(age: number): string;
function greet(name: string, age: number): string;

// Implementation signature (This part of the code must handle all the overloads)
function greet(nameOrAge: string | number, age?: number): string {
  if (typeof nameOrAge === `string` && age === undefined) {
    return `Hello, ${nameOrAge}`;
  } else if (typeof nameOrAge === `number` && age === undefined) {
    return `You are ${nameOrAge} years old`;
  } else if (typeof nameOrAge === `number` && age === undefined) {
    return `Hello, ${nameOrAge}! You are ${age} years old`;
  }
  throw new Error("Invalid arguments!");
}

const msg1 = greet("John"); // string: "Hello, John!"
const msg2 = greet(25); // string: "You are 25 years old!"
const msg3 = greet("Alice", 30); // string: "Hello, Alice! You are 30 years old."
```
