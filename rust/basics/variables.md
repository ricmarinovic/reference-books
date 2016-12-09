# Variables

Variables are immutable by default. To make them mutable, add `mut` before the variable name. Shadowing allows the same variable name to be reused. Rust is a statically typed language with type inference. You can annotate the variable by adding the type like this example:

```rust
let mut five = 5;
let mut five: i32 = 5;
```

## Ownership

Taking ownership using only `v`. At the end of the scope, Rust will clean up everything related to the bound variable, the stack and even the heap-allocated memory. Rust ensures that there is exactly one binding to any given resource.

## Borrowing

A reference `&v` and it borrows ownership instead of owning it. A binding that borrows something does not deallocate the resource when it goes out of scope. References are immutable, like bindings.

A mutable reference `&mut v` allows you to mutate the resource you’re borrowing. There can be only one mutable reference at a time.
