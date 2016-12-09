# Operators

Operators are all defined by the [Kernel module](https://hexdocs.pm/elixir/Kernel.html). Reference for all operators can be found [here](https://hexdocs.pm/elixir/operators.html).

```elixir
=== !== == !=       # Strict and relaxed equality comparison
> >= < <=           # Comparison
and or not && || !  # Strict and relaxed boolean operators
+ - * / div rem     # Arithmetic operators
<> ++ -- ..         # Binary and list concatenation, diff, range
in                  # is the same as Enum.member?/2
```

Comparing different types follow this rule: `number < atom < reference < function < port < pid < tuple < map < list < binary`

The **pipe operator** `|>` gets the result of the left statement and passes it as the first argument to the function on the right.

```elixir
# without using the pipe operator
list = [1, 2, 3, 4, 5]
shuffled = Enum.shuffle(list)
IO.inspect(shuffled)
#=> [3, 4, 5, 1, 2]

# using the pipe operator
[1, 2, 3, 4, 5] |> Enum.shuffle |> IO.inspect
#=> [3, 4, 5, 1, 2]
```

Other operators include:

* `=` [match](variables.html)
* `|` [cons](types.html#list)
* `^` [pin](variables.html)
* `&` [capture](functions.html)
* `?` codepoint: returns the UTF-8 codepoint of the character following it.
* `=~` string match: returns `true` if the string on the left is a substring or a regular expression match of the string on the right.
