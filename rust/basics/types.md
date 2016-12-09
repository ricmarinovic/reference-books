# Types

## Booleans

Booleans are built-in types, named `bool`. [Reference](https://doc.rust-lang.org/std/primitive.bool.html)

```rust
let x = true;
let y: bool = false;
```

## Char

`char` is a single Unicode value. They are created with single-quotes. [Reference](https://doc.rust-lang.org/std/primitive.char.html)

```rust
let x = 'x';
```

## Numbers

All numerical types:

```rust
i8, i16, i32, i64
u8, u16, u32, u64
isize, usize // range is sufficient to express the size of any collection
f32, f64
```

## Arrays

Lists of elements of the same type. [Reference](https://doc.rust-lang.org/std/primitive.array.html)

```rust
let a = [1, 2, 3];
let a: [i32, 3] = [1, 2, 3];
```

## Vectors

A vector is a growable array, implemented as the standard libary type `Vec<T>`. Vectors always allocate their data on the heap at runtime. (?) It is created by the `vec!` macro. Index must be of `usize` type. [Reference](https://doc.rust-lang.org/std/vec/)

```rust
let v = vec![1, 2, 3, 4, 5];
let v: Vec<i32> = vec![1, 2, 3, 4, 5];
let v = vec![3; 10]; // repeating the same value: ten threes
```

`get` and `get_mut` are used to avoid panicking on out-of-bounds errors, return `None` instead.

```rust
let v = vec![1, 2, 3];
match v.get(7) {
  Some(x) => println!("Item 7 is {}", x),
  None => println!("Sorry, this vector is too short."),
}
```

```rust
let mut v = vec![1, 2, 3, 4, 5];

for i in &v { println!("A reference to {}", i); }

for i in &mut v { println!("A mutable reference to {}", i); }

for i in v { println!("Take ownership of the vector and its element {}", i); }
```

### Slices

[Reference](https://doc.rust-lang.org/std/primitive.slice.html)

```rust
let a = [0, 1, 2, 3, 4];
let one = a[1];
let complete = &a[..]; // All elements
let middle = &a[1..4]; // Only elements 1, 2, 3
```

## Tuples

Ordered list of fixed size. Accept different types. [Reference](https://doc.rust-lang.org/std/primitive.tuple.html)

```rust
let x = (1, "hello");
let x: (i32, &str) = (1, "hello");

let tuple = (1, 2, 3);

let a = tuple.0;
```

## String

`str` is the most primitive type.
