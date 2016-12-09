# Control flow

## case

`case` is used to compare a value against many patterns. You can use [guard clauses](functions.html#guard-clauses) when pattern matching with `case`.

```elixir
case {1, 2, 3} do
  {4, 5, 6} ->
    "This clause won't match"
  {1, x, 3} ->
    "This clause will match and bind x to 2 in this clause"
  _ ->
    "This clause would match any value"
end
```

## if and unless

`if` and `unless` are useful to check for only one condition.

```elixir
if true do
  :ok
else
  :error
end
```

## cond

`cond` is useful to check multiple conditions. It is like `else if` in other languages.

```elixir
cond do
  2 + 2 == 5 ->
    "This will not be true"
  1 + 1 == 2 ->
    "But this will"
end
```

## with

`with` is used to combine matching clauses. If all clauses match, the `do` block is executed, otherwise the chain is aborted and the non-matched value is returned. [Guard clauses](functions#guard-clauses) can be used in patterns. An `else` option may be given that will run in case of a failed match. `with` is useful when there are nested `case` statements with error handling. Variables bound inside `with` are restricted to it.

```elixir
with {:ok, width} <- Map.fetch(opts, :width),
     {:ok, height} <- Map.fetch(opts, :height),
  do: {:ok, width * height}
#=> {:ok, 150} if both match
#=> :error if one does not
```

## Comprehensions

Comprehensions are used to loop over one or more collections, extracting values from each, filtering out some results and mapping them into another collection. A comprehension is made of three parts: generators, filters and collectables.

`for generator [, filter] [, into: value], do: expression`

Comprehensions discard all elements for which the filter expression returns false or nil. Variables bound inside `for` are restricted to it.

```elixir
multiple_of_3? = fn (n) -> rem(n, 3) == 0 end

for x <- 0..5, multiple_of_3?.(x) do: x*x
#=> [0, 9]

for {key, val} <- %{"a" => 1, "b" => 2}, into: %{}, do: {key, val * val}
#=> %{"a" => 1, "b" => 4}
```
