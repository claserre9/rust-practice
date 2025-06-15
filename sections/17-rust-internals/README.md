# Rust Internals – MIR, borrow checker internals, trait resolution

## Overview
Understanding Rust’s internals offers deeper insight into how the language works. The Mid-level Intermediate Representation (MIR) is used by the compiler for borrow checking and optimization. The borrow checker enforces memory safety through dataflow analysis, while trait resolution determines how generic functions are instantiated.

## Detailed Explanation
### MIR
MIR sits between the high-level AST and low-level LLVM IR. It simplifies the program into a control-flow graph, enabling optimizations and precise borrow checking. You can inspect MIR using `rustc --emit=mir`.

### Borrow Checker Internals
The borrow checker operates on MIR, tracking lifetimes of references and ensuring they don’t overlap in conflicting ways. It uses dataflow algorithms to enforce rules such as no mutable aliasing and validity of references.

### Trait Resolution
When you call a method on a generic type, the compiler resolves which trait implementation applies by examining trait bounds and where clauses. It uses a system known as coherence to ensure there’s at most one applicable implementation in scope.

## Code Examples
```rust
fn example() {
    let mut x = 5;
    let y = &x; // immutable borrow
    let z = &mut x; // ERROR: cannot borrow `x` as mutable because it is also borrowed as immutable
    println!("{y} {z}");
}
```

To inspect MIR, run:
```bash
rustc --emit=mir src/main.rs -O
```

## Common Pitfalls & Warnings
- **Borrow checker misunderstandings**: Errors can be confusing at first. Use compiler flags like `-Z borrowck=mir` (nightly) for extra debugging information.
- **Trait coherence conflicts**: Implementing a foreign trait for a foreign type is disallowed (the orphan rule) to prevent conflicting implementations.

## Best Practices
- Read the official Rustonomicon for deeper insights into unsafe code and internals.
- Experiment with nightly features in small projects to learn how the compiler works, but avoid them in production without stability guarantees.

## Mini Exercise
Compile a small program with `rustc --emit=mir` and inspect the generated `.mir` files. Identify the control-flow structure for a simple `if` statement and see how variables are represented.
