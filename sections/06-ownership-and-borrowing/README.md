# Ownership and Borrowing – The ownership model, borrowing, references

## Overview
Ownership is Rust’s core concept for managing memory safety without a garbage collector. Each value has a single owner; when the owner goes out of scope, the value is dropped. Borrowing allows references to data without transferring ownership, enabling safe concurrency and reducing unnecessary copies.

## Detailed Explanation
### Ownership Rules
1. Each value in Rust has a variable that’s called its owner.
2. There can be only one owner at a time.
3. When the owner goes out of scope, the value is dropped.

### Borrowing
Borrowing occurs when you pass references to data (`&T` for immutable, `&mut T` for mutable). While references are active, the original owner cannot be moved or, in the case of immutable references, mutated. The compiler checks these rules at compile time, preventing data races and dangling pointers.

### Why It’s Important
Unlike languages with garbage collectors, Rust’s ownership model enables deterministic resource management and zero-cost abstractions. Compared to manual memory management, it removes entire classes of bugs like double frees or memory leaks.

## Code Examples
```rust
fn main() {
    let s = String::from("hello");
    takes_ownership(s); // s is moved here and is no longer valid

    let x = 5;
    makes_copy(x); // x is Copy, so it’s still usable after the call

    let mut s2 = String::from("borrow");
    change(&mut s2); // mutable borrow
    println!("{s2}");
}

fn takes_ownership(some_string: String) {
    println!("{some_string}");
} // some_string is dropped here

fn makes_copy(some_int: i32) {
    println!("{some_int}");
}

fn change(s: &mut String) {
    s.push_str(" me");
}
```

## Common Pitfalls & Warnings
- **Dangling references**: The compiler won’t allow returning references to values created inside the function because they’ll be dropped at the end.
- **Mutable aliasing**: You cannot have more than one mutable reference to a value in the same scope, nor a mutable reference while immutable references exist.

## Best Practices
- Favor references over cloning large data structures to avoid unnecessary allocations.
- Use Rust’s ownership system to manage resources beyond memory, such as file handles or network sockets.

## Mini Exercise
Write a function `first_word(s: &str) -> &str` that returns a slice of the first word in a string. Test it by borrowing a `String` and ensuring that the original string remains usable afterward.
