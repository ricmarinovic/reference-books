# Macros

## Abstract Syntax Tree

Macros in Elixir enable metaprogramming. All Elixir code is represented internally by the abstract syntax tree (AST). Metaprogramming is all about manipulating and inspecting the AST. It is possible to access the AST representation of any Elixir expression using the `quote` macro.

Elixir code is represented by three-element tuples:

* The first is an atom with the function call.
* The second is metadata about the expression.
* The third is a list of arguments for the function call.

Literals are represented in AST as themselves: atom, integers, floats, binaries, lists (including keyword lists) and two-element tuples only.

```elixir
quote do: 1 + 2
#=> {:+, [context: Elixir, import: Kernel], [1, 2]}
```

## Creating macros

`defmacro` is used to create a macro and they must be defined inside modules. Parameters passed to a macro are not evaluated, instead they are passed as the AST representation. Macros take in an AST representation and give back an AST representation.

```elixir
defmodule Kernel do
  defmacro unless(condition, do: clause) do
    quote do
      if unquote(condition), do: nil, else: unquote(clause)
    end
  end
end
```

The `require` function tells Elixir to ensure the module with the macro definition is compiled before the module using that macro. Passing the `bind_quoted` option to the `quote` macro will ensure outside bound variables are unquoted only a single time.

```elixir
defmodule Example do
  defmacro double_puts(expression) do
    quote bind_quoted: [expr: expression] do
      IO.puts expression
      IO.puts expression
    end
  end
end

require Example
Example.double_puts(:os.system_time)
#=> 1480870512774237000
#=> 1480870512774237000
```

It is possible to extend a module with the function [`use/2`](/elixir/2016/11/15/syntax.html#use) adding `use ModuleName`, which invokes the `ModuleName.__using__/1` macro.

## Useful functions and macros

**`Code.eval_quoted(quoted, binding \\ [], opts \\ [])`**

Evaluates the quoted contents. The `binding` argument is a keyword list of variable bindings. The opts argument is a keyword list of environment options.

**`Kernel.var!(var, context \\ nil)`**

When used inside quoting, marks that the given variable should not be hygienized.

The argument can be either a variable unquoted or in standard tuple form {name, meta, context}.
