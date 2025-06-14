# Rust in Production – Tooling (clippy, fmt, cargo-audit, CI/CD tips)

## Overview
Using Rust in production requires robust tooling for code quality and security. Tools like `rustfmt` for formatting, `clippy` for linting, and `cargo-audit` for dependency vulnerability scanning help maintain high standards. Integrating these tools into continuous integration (CI) pipelines ensures consistency and reliability.

## Detailed Explanation
### rustfmt
`rustfmt` automatically formats your code according to style guidelines. Run `cargo fmt` to apply formatting across the project. Consistent formatting improves readability and reduces noise in code reviews.

### clippy
`clippy` is a collection of lints that catch common mistakes and suggest idiomatic Rust patterns. Invoke it with `cargo clippy`. Pay attention to warnings about performance or suspicious code.

### cargo-audit
`cargo-audit` scans `Cargo.lock` for crates with known vulnerabilities. It uses the RustSec advisory database and warns if updates are needed to keep dependencies secure.

### CI/CD Tips
- Add `cargo fmt -- --check` and `cargo clippy -- -D warnings` to your CI pipeline to enforce formatting and linting.
- Run `cargo test` and `cargo audit` as part of automated checks before deploying.
- Use tools like GitHub Actions or GitLab CI for cross-platform testing and releases.

## Code Examples
```yaml
# Example GitHub Actions snippet
name: Rust CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
          override: true
      - run: cargo fmt -- --check
      - run: cargo clippy -- -D warnings
      - run: cargo test
      - run: cargo audit || true
```

## Common Pitfalls & Warnings
- **Ignoring lint warnings**: Treat `clippy` warnings seriously; they often point to real issues.
- **CI drift**: Ensure your local environment matches CI toolchains to avoid unexpected build failures.

## Best Practices
- Keep `Cargo.lock` checked in for applications to ensure reproducible builds.
- Automate checks in CI to catch issues early and maintain code health over time.

## Mini Exercise
Set up a minimal GitHub Actions workflow that runs `cargo fmt -- --check` and `cargo test` on every push. Experiment by adding `clippy` and `cargo-audit` steps.
