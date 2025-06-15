# Testing and Debugging – Unit tests, integration tests, benchmarking, dbg!, cargo test

## Overview
Testing and debugging are integral to reliable software. Rust’s tooling provides built-in support for unit tests, integration tests, and benchmarking. The `dbg!` macro offers quick insight into values during development. The `cargo test` command orchestrates compiling and running tests automatically.

## Detailed Explanation
### Unit Tests
Placed in the same file as the code they test, unit tests focus on small, isolated functionality. They are annotated with `#[test]` and run with `cargo test`.

### Integration Tests
These tests reside in the `tests` directory and exercise your library’s public API as a whole. Each file is compiled as a separate crate, ensuring only public items are accessible.

### Benchmarking
With the `criterion` crate or unstable built-in features, you can measure performance over time. Benchmarks are executed with `cargo bench`.

### Debugging with `dbg!`
The `dbg!` macro prints a value along with the file and line number, returning ownership of the expression. It’s handy for quick inspection during development.

## Code Examples
```rust
// src/lib.rs
pub fn add(a: i32, b: i32) -> i32 { a + b }

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(2, 3), 5);
    }
}
```

```rust
// tests/integration_test.rs
use my_crate::add;

#[test]
fn it_works() {
    assert_eq!(add(1, 2), 3);
}
```

```rust
// Using dbg!
let value = dbg!(some_function());
```

## Common Pitfalls & Warnings
- **Ignoring test failures**: `cargo test` runs all tests; if one fails, inspect the output to diagnose rather than ignoring it.
- **Debug-only code**: Remember to remove or disable `dbg!` calls before final release builds.

## Best Practices
- Keep unit tests small and focused on one behavior.
- Use integration tests to cover public APIs and external behavior.

## Mini Exercise
Create a library crate with a function `square(n: i32) -> i32`. Write a unit test verifying that `square(4)` equals `16` and an integration test calling the public function. Run the tests using `cargo test`.
