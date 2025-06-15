# Concurrency and Multithreading – Threads, Channels, Arc, Mutex

## Overview
Rust’s fearless concurrency model ensures thread safety at compile time. Using the standard library, you can spawn threads, communicate between them with channels, and share data safely with `Arc` and `Mutex`. These primitives enable building concurrent programs without data races.

## Detailed Explanation
### Threads
Threads are created with `std::thread::spawn`, executing a closure in parallel with the current thread. Ownership rules extend across threads; data must be `Send` to move into a new thread and `Sync` to share immutable references.

### Channels
Channels provide message passing between threads. A sender transmits values to a receiver, allowing synchronization without shared state. Use `std::sync::mpsc` for multi-producer, single-consumer channels.

### Arc and Mutex
`Arc<T>` is an atomically reference-counted pointer that allows multiple threads to own the same data. `Mutex<T>` provides interior mutability with locking. Combining `Arc<Mutex<T>>` gives shared, mutable access across threads.

## Code Examples
```rust
use std::sync::{Arc, Mutex, mpsc};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0));
    let (tx, rx) = mpsc::channel();
    let mut handles = vec![];

    for _ in 0..5 {
        let counter = Arc::clone(&counter);
        let tx = tx.clone();
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
            tx.send(*num).unwrap();
        });
        handles.push(handle);
    }

    for handle in handles { handle.join().unwrap(); }
    for received in rx { println!("count = {received}"); }
}
```

## Common Pitfalls & Warnings
- **Deadlocks**: Locking order of mutexes can cause deadlocks. Keep critical sections small and consistent.
- **Cloning channels**: Cloning the transmitter increases the number of senders. Dropping all senders is required to close the channel and allow the receiver to exit loops.

## Best Practices
- Use channels for communicating state rather than sharing mutable data when possible.
- Prefer `Arc<Mutex<T>>` for shared mutable data, but consider `RwLock` for scenarios with many readers and few writers.

## Mini Exercise
Modify the example to spawn 10 threads that each increment the shared counter five times. Send the final value from each thread over the channel and print the sequence of received values.
