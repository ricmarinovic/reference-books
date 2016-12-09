# Functions

Functions can be defined with `def/2` and private functions with `defp/2`. Private functions can only be called within the module it is defined. Functions are also a type. Arity is the number of parameters of a given function: `Enum.map/2`.

The `&` operator can be used to capture functions, passing `&Module.function/arity` or using `&1`, `&2`, etc. as placholders for parameters. More on this [here](https://hexdocs.pm/elixir/Kernel.SpecialForms.html#&/1).

Named functions must be defined inside modules. Defining default values for arguments is possible by adding `\\ default` after the argument on the function definition. It is also possible to use [guard clauses](#guard-clauses) with `when` to refine the match on functions.

```elixir
# Anonymous function (lambdas)
square = fn (x) -> x*x end
# Using the & operator
square = &(&1*&1)

square.(2) #=> 4

# Named function
defmodule Math do
  # Inline definition
  def square(x), do: x*x

  # with do/end blocks (syntactic sugar)
  def multiply(x, y) do
    x * y
  end

  # use \\ to default arguments
  # the following example is using a guard clause
  def divide(x, y \\ 2) when y != 0 do
    x / y
  end
end
```

## Guard clauses

Reference for all allowed guard clauses can be found [here](https://hexdocs.pm/elixir/guards).

Guard clauses can also be used in [case](control-flow.html#case) expressions.

```elixir
# List of allowed guard clauses

=== !== == != > >= < <= # Comparison operators
and or not              # Strict boolean operators
+ - * /                 # Arithmetic operators
<>                      # Binary concatenation
in                      # Membership operator

# The following "type-check" functions defined in the Kernel module
is_atom/1, is_binary/1, is_bitstring/1, is_boolean/1, is_float/1,
is_function/1, is_function/2, is_integer/1, is_list/1, is_map/1,
is_nil/1, is_number/1, is_pid/1, is_port/1, is_reference/1, is_tuple/1

# The following "safe" functions defined in the Kernel Module
abs/1, binary_part/3, bit_size/1, byte_size/1, div/2, elem/2,
hd/1, length/1, map_size/1, node/0, node/1, rem/2, round/1,
self/0, tl/1, trunc/1, tuple_size/1
```
