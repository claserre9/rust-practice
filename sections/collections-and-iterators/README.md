# Collections and Iterators – Vectors, HashMaps, Iterators, Functional Methods

## Overview
Rust offers powerful standard collections and iterator tools. Vectors and HashMaps are dynamic, growable structures, while iterators provide lazy sequences that can be transformed through functional methods like `map`, `filter`, and `fold`. This combination enables expressive and efficient data manipulation.

## Detailed Explanation
### Vectors
Vectors (`Vec<T>`) are resizable arrays. They store elements contiguously in memory and grow as needed. Methods like `push`, `pop`, and indexing make them versatile for dynamic lists.

### HashMaps
`HashMap<K, V>` stores key-value pairs. Keys must implement `Eq` and `Hash`. HashMaps provide efficient lookup, insertion, and removal operations.

### Iterators
Iterators represent a sequence of values. The `Iterator` trait defines methods like `next`, but higher-level adapters allow chaining transformations. Many collections offer iterator creation via `iter()`, `iter_mut()`, or `into_iter()`.

## Code Examples
```rust
use std::collections::HashMap;

fn main() {
    let mut numbers = vec![1, 2, 3];
    numbers.push(4);
    for n in &numbers {
        println!("{n}");
    }

    let mut scores = HashMap::new();
    scores.insert("alice", 10);
    scores.insert("bob", 8);

    if let Some(score) = scores.get("alice") {
        println!("alice: {score}");
    }

    let sum: i32 = numbers.iter().map(|x| x * 2).sum();
    println!("sum = {sum}");
}
```

## Common Pitfalls & Warnings
- **HashMap iteration order**: Iteration order is undefined; don’t rely on insertion order.
- **Iterator consumption**: Calling iterator methods like `collect` or `sum` consumes the iterator; it cannot be reused without re-creating it.

## Best Practices
- Use iterator chains for concise and expressive data processing.
- Prefer `Vec` over arrays for dynamic collections, and reserve `HashMap` for associative lookups.

## Mini Exercise
Create a vector of integers from 1 to 10. Use iterator methods to filter out the even numbers, square the remaining ones, and collect the results into a new vector. Print the final vector.
