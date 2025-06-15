# Introduction to Rust – Installing Rust and Writing Your First Program

## Overview
Rust is a modern systems programming language focused on safety and performance. It eliminates entire classes of bugs by enforcing strict compile-time checks, while also providing low-level control similar to C or C++. Getting started requires installing the Rust toolchain and writing a simple program to understand the basic workflow. This section walks you through the installation process and demonstrates how to compile and run a basic program.

## Detailed Explanation
Rust uses the `rustup` tool to manage versions and associated utilities like `cargo`—Rust’s package manager and build system. Once installed, you can create new projects or compile single files. The compiler enforces memory safety without needing a garbage collector, leading to predictable performance. Compiled binaries are statically linked by default, making deployment straightforward across environments.

### How It Works
1. Install `rustup`, which includes the Rust compiler (`rustc`) and `cargo`.
2. Use `cargo new` to create a new project. This generates a `Cargo.toml` manifest and a sample `src/main.rs`.
3. Run `cargo build` or `cargo run` to compile and execute your program. Cargo handles dependency resolution, compilation, and running tests.

### Importance
Rust’s installation and workflow are the gateway to the language’s unique benefits. Compared to scripting languages, Rust requires a compile step, but in exchange you get type safety, memory safety, and optimized performance. Cargo’s integration of dependency management, testing, and build scripts fosters a streamlined experience similar to high-level languages but with the power of low-level control.

## Code Examples
```bash
# Install rustup (Linux/macOS)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

```bash
# Windows (PowerShell)
Invoke-WebRequest -Uri https://sh.rustup.rs -UseBasicParsing | Invoke-Expression
```

```bash
# Create and run a new project
cargo new hello_rust
cd hello_rust
cargo run
```

```rust
// src/main.rs
fn main() {
    println!("Hello, Rust!");
}
```

## Common Pitfalls & Warnings
- **Skipping `rustup`**: Installing Rust via other methods can lead to outdated toolchains. Always use `rustup` unless using a system package specifically managed by your organization.
- **Forgetting to update**: Run `rustup update` periodically to stay current with the stable release.

## Best Practices
- Use `cargo run` during development for quick feedback.
- Keep your toolchain up to date, but lock versions for production builds using `rust-toolchain.toml`.

## Mini Exercise
1. Install Rust using `rustup`.
2. Create a project named `greeting` with `cargo new`.
3. Modify `src/main.rs` so the program prints your own custom greeting.
4. Build and run the program with `cargo run`.
