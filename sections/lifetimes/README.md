# Lifetimes – Lifetime annotations, elision rules, real-world use cases

## Overview
Lifetimes are Rust’s way of ensuring that references remain valid. They describe the scope for which a reference is valid and prevent dangling pointers. While many lifetimes are inferred, some situations require explicit annotations to disambiguate how long references should live.

## Detailed Explanation
### Lifetime Annotations
Lifetimes are written using apostrophe syntax like `'a`. Functions that accept references with potentially different lifetimes may need annotations to relate them. For instance, `fn longest<'a>(x: &'a str, y: &'a str) -> &'a str` tells the compiler that the returned reference will live as long as both input references.

### Elision Rules
Rust has three lifetime elision rules that allow omitting explicit lifetimes in common cases:
1. Each parameter that is a reference gets its own lifetime parameter.
2. If there is exactly one input lifetime, that lifetime is assigned to all output lifetimes.
3. If there are multiple input lifetimes but one of them is `&self` or `&mut self`, the lifetime of `self` is assigned to all output lifetimes.

### Real-World Use Cases
Lifetimes appear often in functions returning references to data passed in or stored in structs with references. They also surface in iterator implementations and asynchronous code where references span multiple scopes.

## Code Examples
```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() { x } else { y }
}

fn main() {
    let s1 = String::from("abcd");
    let s2 = "xyz";
    let result = longest(&s1, s2);
    println!("Longest: {result}");
}
```

## Common Pitfalls & Warnings
- **Dangling references**: The compiler will prevent returning a reference that outlives its source data.
- **Over-specifying lifetimes**: Adding unnecessary lifetime annotations can make code harder to read; rely on elision rules when possible.

## Best Practices
- Start by writing code without explicit lifetimes and add them only when the compiler requires it.
- Name lifetimes meaningfully in complex scenarios (`'a`, `'b`) to clarify relationships between references.

## Mini Exercise
Write a struct `Book<'a>` containing a reference to a `str` title. Implement a method `announce(&self)` that prints the title. Instantiate a `Book` and call `announce()` to demonstrate how lifetimes enable borrowing data from the outside.
