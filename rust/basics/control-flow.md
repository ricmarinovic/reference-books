# Control flow

## if/else

```rust
let x = 5;

if x == 5 {
  println!("x is five!");
} else if x == 6 {
  println!("x is six!");
} else {
  println!("x is not five nor six");
}
```

## loop

```rust
loop {
  // infinite loop
}
```

## while

```rust
let mut done = false;

while !done {
  // do this
}
```

## for

```rust
for var in expression {
  // do this
}
```

`expression` can be converted into an iterator using `IntoIterator`. The `.enumerate()` function keeps track of how many times it was looped.

```rust
for (index, value) in (5..10).enumarate() {
  println!("index = {} and value = {}", index, value);
}
```
