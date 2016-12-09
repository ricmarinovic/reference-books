
## Behaviours

Behaviours define a set of functions that must be implemented by a module and ensure that a module implements all functions in that set. It separates the generic part of a component (the *behaviour* module) from the specific part (the *callback* module).

```elixir
defmodule MyBehaviour do
  @callback vital_fun() :: any
  @callback non_vital_fun() :: any
  @macrocallback non_vital_macro(arg :: any) :: Macro.t
  @optional_callbacks non_vital_fun: 0, non_vital_macro: 1
end
```

```elixir
defmodule MyCallbackModule do
  @behaviour MyBehaviour
  def vital_fun(arg), do: arg
end
```

The built-in behaviours are:

* [Access](https://hexdocs.pm/elixir/Access.html)
* [Application](https://hexdocs.pm/elixir/Application.html)
* [Calendar](https://hexdocs.pm/elixir/Calendar.html)
* [Exception](https://hexdocs.pm/elixir/Exception.html)
* [GenServer](https://hexdocs.pm/elixir/GenServer.html)
* [Supervisor](https://hexdocs.pm/elixir/Supervisor.html)
