# Angular-Notes

## TypeScript Overview

## Introduction
TypeScript is a superset of JavaScript that offers type safety and compiles down to JavaScript. It provides additional features to JavaScript developers, making code more robust and maintainable.

## Features
1. **Type Safety**: TypeScript introduces static typing, allowing developers to define types for variables, parameters, and return values. This helps catch type-related errors during development rather than at runtime.
2. **Data Types**:
   - `string`: `let name: string = "Santos"`
   - `number`: `let age: number = 23`
   - `boolean`: `let isAdult: boolean = false`
   - Arrays: `let list: string[] = ["a", "b", "c"]` or `let list: Array<string> = ["a", "b", "c"]`
   - Enumerations: 
     ```typescript
     const enum Color {
         Red,
         Green,
         Blue
     }
     let c: Color = Color.Blue;
     ```
     Note: Using `const` with `enum` trims the type-related code when deployed to production.
   - `any`: Avoid using `any` whenever possible as it undermines TypeScript's type safety.
   - `void`: Represents the absence of a type, often used as the return type for functions that do not return a value.
   - `never`: Represents the type of values that never occur, such as a function that always throws an error or never returns.

3. **Type Inference**: TypeScript can infer types when they're not explicitly specified, reducing the need for verbose type annotations.
   
4. **Functions**:
   - Basic function:
     ```typescript
     function add(num1: number, num2: number) {
         return num1 + num2;
     }
     ```
     If you forget to include a return statement, TypeScript won't throw an error.
   - Typed function:
     ```typescript
     function add(num1: number, num2: number): number {
         return num1 + num2;
     }
     ```
     In this case, if the return keyword is omitted or if the return type mismatches, TypeScript will highlight the issue, providing better error detection.
   - Arrow function:
     ```
     const sub = (num1: number, num2: number) => {
        return num1 - num2;
     }
     ```
  - Optional Parameters:
    ```
    function greet(name?: string) {
    if (name) {
        return `Hello, ${name}!`;
    } else {
        return 'Hello!';
    }
   }
   ```
Optional parameters can be specified using a question mark (?), allowing flexibility in function calls.
 - Default Parameters
   ```
   function greet(name: string = 'World') {
    return `Hello, ${name}!`;
   }
   ```
Default parameter values are assigned if no argument is provided during the function call.
- Rest Parameters
  ```
   function addAll(...nums: number[]): number {
    return nums.reduce((total, num) => total + num, 0);
}

const numbers = [1, 2, 3, 4, 5];
console.log(addAll(...numbers)); 
```
   Rest parameters allow functions to accept any number of arguments as an array.

- Generic Functions
```
function getItems<T>(items: T[]): T[] {
    return new Array<T>().concat(items);
}

let concatResult = getItems<number>([1, 2, 3, 4, 5]);
let concatString = getItems<string>(["a", "b", "c", "d", "e"]);
```
Generic functions enable writing reusable code that works with different types.
