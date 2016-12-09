# Functions

Parameters must declare their types. Returns of functions are also decrared after a arrow `->`. The last expression of a function is returned and it must not have a semicolon.

```rust
fn print_number(x: i32, y: i32) -> i32 {
  x + y
}
```

Function pointers are used to create variable bindings which point to functions.

```rust
fn plus_one(i: i32) -> i32 {
  i + 1
}

let f = plus_one; // with type inference
let f: fn(i32) -> i32 = plus_one; // without type inference

let six = f(5);
```
