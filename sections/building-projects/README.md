# Building Projects – CLI tools, REST APIs, WASM, and game engines (bevy)

## Overview
Rust’s ecosystem supports diverse application domains. You can build command-line tools, web services, WebAssembly (WASM) modules, and games using frameworks like Bevy. This section highlights the key concepts and crates involved in these areas.

## Detailed Explanation
### CLI Tools
`clap` or `argh` help you parse command-line arguments and options. Combine them with `structopt` for deriving argument parsing from struct definitions. `cargo install` lets you distribute CLI binaries easily.

### REST APIs
Frameworks such as `actix-web` and `axum` allow building fast, type-safe web services. They integrate with `serde` for JSON serialization and `tokio` for async operations.

### WebAssembly
Rust compiles to WASM via `wasm32-unknown-unknown` target. Tools like `wasm-bindgen` facilitate interaction between Rust and JavaScript. WASM is ideal for high-performance web apps or running Rust in browsers.

### Game Engines
Bevy is an ECS (Entity Component System) game engine written in Rust. It provides cross-platform rendering, audio, and input support. You write systems in Rust and rely on Bevy’s scheduler to manage them.

## Code Examples
```rust
// CLI example with clap
use clap::Parser;
#[derive(Parser)]
struct Args { name: String }
fn main() {
    let args = Args::parse();
    println!("Hello, {}!", args.name);
}
```

```rust
// Basic REST API using axum
use axum::{routing::get, Router};
#[tokio::main]
async fn main() {
    let app = Router::new().route("/", get(|| async { "Hello" }));
    axum::Server::bind(&"0.0.0.0:3000".parse().unwrap())
        .serve(app.into_make_service())
        .await
        .unwrap();
}
```

## Common Pitfalls & Warnings
- **Target confusion**: Building for WASM or other platforms requires the correct target triple (`wasm32-unknown-unknown`, etc.).
- **Binary size**: Minimize release binary size by using `--release` and features like `strip` or `opt-level`.

## Best Practices
- Use `cargo new --bin` for CLI projects and `cargo generate` for templates when starting larger applications.
- Separate business logic from I/O code for easier testing and maintenance.

## Mini Exercise
Create a simple CLI program that accepts a `--name` argument and prints a personalized greeting. Then, modify it to compile to WebAssembly using `wasm-pack` and run it in a web page.
