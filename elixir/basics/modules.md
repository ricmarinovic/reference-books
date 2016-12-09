# Modules

Modules provides namespace for functions. Named functions must be defined inside modules.

```elixir
defmodule Timer do
  def set, do: alert(Time.new(1, 28, 00, 0,  0}))
  defp alert(time), do: "Wake me up at #{time}"
end
```

## Module attributes

Module attributes are variables defined inside modules (not functions) used to annotate the module and as constants. Attributes can be read inside functions. The value exists only during compilation time. `@vsn 2` is an example of module attribute.

| Reserved attributes | Description                            |
| :------------------ | :------------------------------------  |
| `@moduledoc` | provides documentation for the current module |
| `@doc` | provides documentation for the function or macro that follows the attribute |
| `@derive` | use a protocol in the module |
| `@before_compile` | provides a hook that will be invoked before the module is compiled |
| `@enforce_keys` | keys that are mandatory when creating a struct |
| `@type` | used to define new types |
| `@typep` | used to define new private types |
| `@opaque` | used to define a public type where the internal structure is not visible |
| `@spec` | used to define functions |
| `@behaviour` | used for specifying an OTP or user-defined behaviour |
| `@callback` | used to define function callbacks of behaviours |
| `@macrocallback` | used to define macro callbacks of behaviours |

Reference for Typespecs can be found [here](https://hexdocs.pm/elixir/typespecs.html).

## alias

Module names can be aliased.

```elixir
alias Module.Name # Defaults to Name
alias Module.Name, as: OtherName
alias Module.{Name1, Name2} # Aliasing multiple modules
```

## import

Summons functions and macros. `import` allows easy access to functions and macros from other modules without using the qualified name. By default functions starting with underscore are not imported and must be explicitly included with the `:only` selector.

```elixir
import ModuleName, only: [this: 1]
import ModuleName, except: [this: 1]
import ModuleName, only: :functions
import ModuleName, only: :macros
```

## require

Summons macros. Makes sure the module is compiled and loaded.

## use

Adds capabilities to a module. It invokes the macro `__using__/1` from the module and the returned quoted code is inserted where `use/2` is called.

```elixir
use Module, some: :options
# is the same as
require Module
Module.__using__([some: :options])
```
