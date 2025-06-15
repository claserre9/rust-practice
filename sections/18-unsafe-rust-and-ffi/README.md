# Unsafe Rust and FFI – unsafe, raw pointers, FFI with C

## Overview
Rust’s `unsafe` keyword enables operations that bypass the compiler’s usual guarantees, allowing low-level memory manipulation and interoperability with foreign languages like C. Used carefully, it unlocks capabilities otherwise impossible in safe Rust.

## Detailed Explanation
### `unsafe` Blocks
Inside an `unsafe` block, you can dereference raw pointers, call `unsafe` functions, access mutable statics, and perform other unchecked operations. The `unsafe` keyword tells the compiler that you, the programmer, uphold the necessary invariants.

### Raw Pointers
Raw pointers (`*const T`, `*mut T`) are similar to C pointers. They can be created from references using `as` casts, but accessing or dereferencing them is only allowed within `unsafe` blocks.

### FFI with C
Rust can interface with C code using the `extern` keyword and `#[link]` attributes. You define function signatures that match the C ABI and link against the appropriate library.

## Code Examples
```rust
extern "C" {
    fn abs(input: i32) -> i32;
}

fn main() {
    unsafe {
        let val = abs(-3);
        println!("abs(-3) = {val}");
    }
}
```

```rust
// Raw pointer usage
let mut num = 5;
let r1 = &num as *const i32;
let r2 = &mut num as *mut i32;
unsafe {
    println!("{}", *r1);
    *r2 = 10;
}
```

## Common Pitfalls & Warnings
- **Undefined behavior**: Misusing `unsafe` can cause memory corruption or crashes. Limit the scope of `unsafe` code and document invariants.
- **FFI mismatch**: Incorrect signatures or calling conventions when interfacing with C can lead to subtle bugs.

## Best Practices
- Encapsulate `unsafe` code in safe abstractions so callers don’t need to use `unsafe` themselves.
- Use crates like `bindgen` to generate bindings for C libraries automatically.

## Mini Exercise
Write an `unsafe` function `split_at_mut` that takes a mutable slice and splits it into two mutable slices at a given index. Ensure it maintains aliasing rules by using raw pointers internally.
