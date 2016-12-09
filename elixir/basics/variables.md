# Variables

Elixir is a dynamic language and the type of a variable is determined by the value it holds. Pattern matching is done using the **match operator** `=`. You can use it to assign values to variables. Variables can be bound only once per match but can be reassigned in subsequent matches. Starting a variable with the **pin operator** `^` will force the variable to its existing value.

Variables starting with `_` are marked as unused variables and not using them will not raise any warning by the compiler. A single `_` will ignore values in pattern matching.

Variable names and functions have the following syntax: A lowercase ASCII letter or an underscore, followed by any number of lowercase or uppercase ASCII letters, numbers, or underscores. Optionally they can end in either an exclamation mark or a question mark.

See the reference for [naming conventions](https://hexdocs.pm/elixir/naming-conventions.html).
