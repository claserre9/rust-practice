# Variables and Data Types – Variables, Constants, Shadowing, Primitive Types

## Overview
Rust enforces strict rules around variable binding and data types to ensure safety and predictability. Variables are immutable by default, though they can be declared mutable. Shadowing allows redeclaring a variable name, while constants provide globally accessible values that cannot change. Rust’s primitive types include integers, floating-point numbers, booleans, characters, and tuples.

## Detailed Explanation
Variables in Rust are immutable unless declared with `mut`. This eliminates many accidental mutations. Shadowing introduces a new variable with the same name, allowing transformation or type changes. Constants are always immutable and must have type annotations. Rust’s type system is static but includes type inference when possible.

### Primitive Types
- **Integers**: `i8`, `u8`, `i16`, `u16`, `i32`, `u32`, `i64`, `u64`, `i128`, `u128`, `isize`, `usize`.
- **Floating Point**: `f32`, `f64`.
- **Boolean**: `bool`.
- **Character**: `char` (Unicode scalar value).
- **Compound Types**: tuples and arrays.

The compiler checks for overflow in debug mode and panics when it occurs; in release mode, overflow wraps around by default.

## Code Examples
```rust
fn main() {
    let x = 5;           // immutable
    let mut y = 10;      // mutable
    y += 5;              // y is now 15

    const SECONDS_IN_DAY: u32 = 60 * 60 * 24;

    let x = x * 2;       // shadowing; x becomes 10
    println!("x = {}, y = {}", x, y);
    println!("There are {SECONDS_IN_DAY} seconds in a day");

    // tuple destructuring
    let point: (i32, i32) = (3, 4);
    let (x_coord, y_coord) = point;
    println!("({x_coord}, {y_coord})");
}
```

## Common Pitfalls & Warnings
- **Uninitialized variables**: Rust will not compile code where a variable might be used before being initialized.
- **Shadowing vs. mutability confusion**: Shadowing creates a new binding; it does not make a variable mutable. Attempting to mutate after shadowing without `mut` will fail.

## Best Practices
- Prefer immutability; only use `mut` when necessary.
- Name constants in screaming snake case (`UPPER_CASE_WITH_UNDERSCORES`).

## Mini Exercise
Write a program that declares a mutable variable `count`, increments it inside a loop until it reaches 5, and prints the value on each iteration. Try shadowing `count` with a new binding that doubles its value, then print the result.
