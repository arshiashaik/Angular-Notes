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

## Conclusion
TypeScript enhances JavaScript by adding static typing and other advanced features, improving code quality and maintainability. It's widely adopted in modern web development, especially in frameworks like Angular.
