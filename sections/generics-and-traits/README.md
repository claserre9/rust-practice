# Generics and Traits – Generics, Traits, Trait Bounds, Polymorphism

## Overview
Generics and traits allow you to write flexible, reusable code. Generics parameterize types so functions and structs can work with any type that meets certain bounds. Traits define shared behavior and enable polymorphism across different types.

## Detailed Explanation
### Generics
Generic functions or structs use type parameters like `T` to represent any type. The compiler monomorphizes generics at compile time, creating concrete implementations for each used type, so there is no runtime cost.

### Traits
Traits are collections of methods that define behavior. Types implement traits to opt into that behavior. Standard traits like `Display`, `Debug`, and `Clone` are used throughout the standard library. Traits can also include default method implementations.

### Trait Bounds
To restrict generic types, you specify trait bounds using syntax like `T: Display`. Multiple bounds use the `+` operator. Where clauses (`where T: Display`) can enhance readability for complex bounds.

### Polymorphism
Rust uses trait objects (`dyn Trait`) for dynamic dispatch when you need runtime polymorphism. This incurs a small runtime cost and requires traits to be object-safe.

## Code Examples
```rust
use std::fmt::Display;

fn largest<T: PartialOrd + Copy>(list: &[T]) -> T {
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }
    largest
}

trait Summary {
    fn summarize(&self) -> String;
}

struct News {
    headline: String,
}

impl Summary for News {
    fn summarize(&self) -> String {
        format!("News: {}", self.headline)
    }
}

fn notify(item: &impl Summary) {
    println!("{}", item.summarize());
}

fn main() {
    let numbers = vec![1, 3, 2];
    println!("largest = {}", largest(&numbers));

    let news = News { headline: String::from("Rust 1.70 Released!") };
    notify(&news);
}
```

## Common Pitfalls & Warnings
- **Trait object safety**: Not all traits can be turned into trait objects. Methods that use `Self` in their signatures or are generic themselves are not object-safe.
- **Complex bounds**: Overly verbose bounds can reduce readability; consider using `where` clauses.

## Best Practices
- Keep trait interfaces small and focused.
- Use generics to reduce code duplication, but don’t over-generalize if only one type is expected.

## Mini Exercise
Define a trait `Area` with a method `area(&self) -> f64`. Implement it for a `Rectangle { width: f64, height: f64 }` and a `Circle { radius: f64 }`. Write a function that takes a slice of trait objects `&[&dyn Area]` and prints the area of each shape.
