# Macros and Metaprogramming – macro_rules!, procedural macros, derive

## Overview
Macros extend Rust’s syntax, enabling code generation and metaprogramming. Declarative macros (`macro_rules!`) let you write pattern-matching rules that expand into code. Procedural macros operate on the abstract syntax tree, providing custom derives, attributes, or function-like macros.

## Detailed Explanation
### `macro_rules!`
Declarative macros use pattern matching to transform input tokens into Rust code. They are defined with `macro_rules!` and expanded at compile time. Each rule matches an invocation pattern and replaces it with generated code.

### Procedural Macros
Procedural macros are functions that receive Rust code as input and output new code. They come in three forms:
1. **Derive macros**: Used with `#[derive]` to automatically implement traits.
2. **Attribute macros**: Modify the item they’re attached to.
3. **Function-like macros**: Look like function calls but operate on tokens.
These macros require a dedicated crate with the `proc-macro` attribute.

## Code Examples
```rust
// Declarative macro
macro_rules! repeat {
    ($val:expr, $times:expr) => {{
        let mut v = Vec::new();
        for _ in 0..$times { v.push($val); }
        v
    }};
}

fn main() {
    let values = repeat!(1, 3);
    println!("{:?}", values);
}
```

```rust
// Procedural macro crate (simplified)
use proc_macro::TokenStream;
#[proc_macro_attribute]
pub fn my_attr(_attr: TokenStream, item: TokenStream) -> TokenStream {
    item
}
```

## Common Pitfalls & Warnings
- **Debugging difficulty**: Macro expansions can be hard to read. Use `cargo expand` to inspect the generated code.
- **Compilation errors**: Macros run at compile time; errors inside them can produce cryptic messages.

## Best Practices
- Keep macros small and focused on removing boilerplate.
- Prefer regular functions or traits when they suffice; macros should be a last resort for code generation.

## Mini Exercise
Create a simple `vec_of_strings!` declarative macro that takes any number of expressions and returns a `Vec<String>` by calling `.to_string()` on each argument.
