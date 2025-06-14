# Async Programming – async, await, Futures, tokio, async-std

## Overview
Asynchronous programming in Rust enables handling many tasks concurrently without blocking threads. The `async` and `await` keywords work with `Future` objects, representing values that may not be available yet. Popular runtime crates like `tokio` and `async-std` provide executors and utilities for writing asynchronous code.

## Detailed Explanation
### Futures
A `Future` is a trait that produces a value asynchronously. Futures are lazy; nothing happens until they are polled by an executor. The `async` keyword creates a state machine implementing `Future` under the hood.

### `async`/`await`
Functions marked `async` return a `Future`. Using `await` pauses execution until the future is ready, yielding control back to the executor so it can run other tasks.

### Async Runtimes
`tokio` and `async-std` are the most widely used runtimes. They schedule and run futures on event loops, provide I/O, timing, and synchronization primitives tailored for asynchronous environments.

## Code Examples
```rust
use tokio::time::{sleep, Duration};

async fn say_after(delay: u64, msg: &str) {
    sleep(Duration::from_secs(delay)).await;
    println!("{msg}");
}

#[tokio::main]
async fn main() {
    let hello = say_after(2, "hello");
    let world = say_after(1, "world");
    tokio::join!(hello, world);
}
```

## Common Pitfalls & Warnings
- **Blocking in async**: Calling blocking operations inside `async` functions can stall the executor. Use async-aware versions (`tokio::fs`, `tokio::task::spawn_blocking`).
- **Runtime mismatch**: Futures created for one runtime (e.g., tokio) may not run on another without compatibility features.

## Best Practices
- Structure asynchronous code as small tasks to keep the event loop responsive.
- Choose a single runtime for your project to avoid compatibility issues.

## Mini Exercise
Implement an async function that fetches two URLs concurrently using `reqwest` and prints the length of the responses. Run it with `tokio::main`.
