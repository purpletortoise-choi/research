## Basic Types
### Boolean
```ts
let isDone: boolean = false;
```
### Number
```ts
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```
### String
```ts
let color: string = "blue";
color = 'red';
```
### Array
```ts
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```
### Tuple
Tuple types allow you to express an array where the type of a fixed number of elements is known, but need not be the same. For example, you may want to represent a value as a pair of a string and a number:
```ts
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error
```
When accessing an element with a known index, the correct type is retrieved:
```ts
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
```
When accessing an element outside the set of known indices, a union type is used instead:
```ts
x[3] = "world"; // OK, 'string' can be assigned to 'string | number'
console.log(x[5].toString()); // OK, 'string' and 'number' both have 'toString'

x[6] = true; // Error, 'boolean' isn't 'string | number'
```
Union types are an advanced topic that we’ll cover in a later chapter
### Enum
```ts
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;

enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName); // Displays 'Green' as its value is 2 above
```
### Any
```ts
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```
### Void
void is a little like the opposite of any: the absence of having any type at all. You may commonly see this as the return type of functions that do not return a value:
```ts
function warnUser(): void {
    console.log("This is my warning message");
}
```
Declaring variables of type void is not useful because you can only assign undefined or null to them:
```ts
let unusable: void = undefined
```
### Null and Undefined
```ts
let u: undefined = undefined;
let n: null = null;
```
### Never
The never type represents the type of values that never occur. For instance, never is the return type for a function expression or an arrow function expression that always throws an exception or one that never returns; Variables also acquire the type never when narrowed by any type guards that can never be true.

The never type is a subtype of, and assignable to, every type; however, no type is a subtype of, or assignable to, never (except never itself). **Even any isn’t assignable to never.**

Some examples of functions returning never:
```ts
// Function returning never must have unreachable end point
function error(message: string): never {
    throw new Error(message);
}

// Inferred return type is never
function fail() {
    return error("Something failed");
}

// Function returning never must have unreachable end point
function infiniteLoop(): never {
    while (true) {
    }
}
```
### Object
object is a type that represents the non-primitive type.
With object type, APIs like Object.create can be better represented. For example:
```ts
declare function create(o: object | null): void;

create({ prop: 0 }); // OK
create(null); // OK

create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```

### Type assertiion
```ts
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;

let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```
