## Agents

Agents are simple abstractions around state.

```elixir
{:ok, count} = Agent.start(fn () -> 0 end)
#=> {:ok, #PID<0.108.0>}
Agent.get(count, &(&1))
#=> 0
Agent.update(count, &(&1+1))
#=> :ok
Agent.get_and_update(count, &({&1+1, &1+1}))
#=> 2
```
