# Error Handling – Result, Option, ?, Custom Errors

## Overview
Rust emphasizes explicit error handling through the `Result` and `Option` types. `Result` is used for recoverable errors, while `Option` represents the presence or absence of a value. The `?` operator simplifies propagating errors, and you can create custom error types to provide richer context.

## Detailed Explanation
### `Result<T, E>`
`Result` is an enum with variants `Ok(T)` and `Err(E)`. Functions that may fail return `Result`, forcing the caller to handle success or failure explicitly. Pattern matching or the `?` operator can be used to extract values.

### `Option<T>`
`Option` has `Some(T)` and `None` variants. It indicates the absence of a value without resorting to `null` pointers. Pattern matching or methods like `unwrap_or` and `map` help handle `Option` safely.

### The `?` Operator
The `?` operator returns early if the `Result` is `Err`, automatically converting compatible error types. It helps reduce boilerplate when propagating errors.

### Custom Errors
Custom error types implement `std::error::Error` and usually derive `Debug` and `Display`. Libraries like `thiserror` can simplify creating them.

## Code Examples
```rust
use std::{fs::File, io::{self, Read}};

fn read_username() -> Result<String, io::Error> {
    let mut file = File::open("username.txt")?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    Ok(contents)
}

fn main() {
    match read_username() {
        Ok(name) => println!("Username: {name}"),
        Err(e) => eprintln!("Error: {e}")
    }
}
```

## Common Pitfalls & Warnings
- **Unwrapping without care**: Using `unwrap()` on `Result` or `Option` will panic on failure; avoid it in production code.
- **Ignoring errors**: The compiler warns if a `Result` is unused. Use `let _ =` only when ignoring is truly intentional.

## Best Practices
- Propagate errors with `?` for readability.
- Use custom error types to provide context and implement `From` for automatic conversions.

## Mini Exercise
Write a function that parses integers from a string, returning `Result<Vec<i32>, std::num::ParseIntError>`. Use `?` to handle potential parsing errors and test the function with valid and invalid input.
