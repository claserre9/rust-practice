# Structs and Enums – Structs, Enums, Pattern Matching

## Overview
Structs and enums allow you to create custom data types in Rust. Structs group related fields together, while enums represent a value that can be one of several variants. Pattern matching with `match` enables ergonomic handling of these user-defined types.

## Detailed Explanation
### Structs
Structs are similar to structs in C or classes without methods in other languages. They let you organize data into named fields. Rust also has tuple structs and unit-like structs for different use cases.

### Enums
Enums define a type by enumerating its possible variants. Variants can be unit-like, tuple-like, or struct-like, each potentially holding different data. Enums are often paired with pattern matching to handle different variants.

### Pattern Matching
Using `match`, you can destructure structs and enums, binding their inner data to variables. The compiler ensures that all possible variants are handled.

## Code Examples
```rust
struct User {
    username: String,
    email: String,
    active: bool,
}

enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn process(msg: Message) {
    match msg {
        Message::Quit => println!("Quit"),
        Message::Move { x, y } => println!("move to ({x}, {y})"),
        Message::Write(text) => println!("{text}"),
        Message::ChangeColor(r, g, b) => println!("color = ({r}, {g}, {b})"),
    }
}

fn main() {
    let user = User {
        username: String::from("alice"),
        email: String::from("alice@example.com"),
        active: true,
    };
    println!("{}", user.username);

    let msg = Message::Move { x: 10, y: 20 };
    process(msg);
}
```

## Common Pitfalls & Warnings
- **Uninitialized struct fields**: All fields must be initialized when creating a struct instance.
- **Missing match arms**: When matching on enums, the compiler forces exhaustive matches to avoid undefined behavior.

## Best Practices
- Use `derive(Debug)` for structs and enums when debugging or logging.
- Prefer enums over complicated boolean flags to represent distinct states.

## Mini Exercise
Create an enum `Shape` with variants `Circle(f64)` and `Rectangle{width: f64, height: f64}`. Write a function `area` that returns the area of a shape. Use pattern matching to calculate areas for both variants.
