# Control Flow – if, match, loops, conditionals

## Overview
Control flow lets you dictate how your program executes based on conditions or repetition. Rust provides familiar constructs like `if`/`else`, pattern matching with `match`, and looping mechanisms such as `loop`, `while`, and `for`. These tools allow you to express branching logic and repetition in a type-safe manner.

## Detailed Explanation
### `if` Statements
`if` expressions evaluate to a boolean and execute a block if true. They can include an `else` block or chain with `else if`. Because `if` is an expression, it can be used in variable bindings.

### `match` Statements
`match` offers powerful pattern matching, evaluating an expression and executing code for the first matching arm. Patterns can destructure enums, tuples, or primitives, ensuring exhaustive coverage at compile time.

### Loops
- **`loop`**: Runs indefinitely until you explicitly `break` out.
- **`while`**: Continues while a condition evaluates to true.
- **`for`**: Iterates over an iterator (like ranges or collections) and is the most idiomatic for fixed loops.

## Code Examples
```rust
fn main() {
    let number = 7;
    if number % 2 == 0 {
        println!("even");
    } else {
        println!("odd");
    }

    match number {
        1 => println!("one"),
        2 | 3 | 5 | 7 | 11 => println!("prime"),
        _ => println!("something else"),
    }

    for i in 0..3 {
        println!("i = {i}");
    }

    let mut count = 0;
    while count < 3 {
        println!("count = {count}");
        count += 1;
    }
}
```

## Common Pitfalls & Warnings
- **Forgetting `break` in a `loop`**: Without a terminating condition, `loop` will run forever.
- **Non-exhaustive `match` arms**: The compiler will prevent missing cases, but using `_` for catch-all may hide unexpected values.

## Best Practices
- Prefer `for` loops when iterating over collections.
- Use pattern matching with `match` for enums instead of complex `if` chains.

## Mini Exercise
Write a program that iterates through numbers 1 to 20. For multiples of 3, print “Fizz”; for multiples of 5, print “Buzz”; for numbers divisible by both, print “FizzBuzz”. Use a `for` loop and `match` statement together to perform the checks.
