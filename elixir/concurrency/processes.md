# Processes

Elixir uses the Actor model of concurrency. Each actor is an independent process performing a specific task, communicating through sending and receiving messages. Processes do not share any information with other processes and are specific about what messages they will act on.

## Creating processes

A new process is created using the Kernel functions `spawn`, `spawn_link` and `spawn_monitor`. The `Kernel.self/0` function will return the pid of the current process.

## Exchanging messages

Messages are sent using the Kernel function `send/2` and received with the Kernel.SpecialForms function `receive/1`. When a message is sent to a process, the message is stored in the process mailbox.

```elixir
send(pid, {:ok, "My message"})
```
```elixir
receive do
  {:ok, message} -> IO.puts message
after 1_000 ->
  IO.puts "No message."
end
```

## Naming processes

* `Process.register(pid, name)` registers the atom name with the given pid.
* `Process.whereis(name)` returns the pid of the registered process.

A `:name` option can be passed to Agents and GenServers `start_link`.

To register a name globally and across [nodes](#nodes), use:

* `:global.register_name(name, pid)`
* `:global.whereis_name(name)`

# Nodes

Starting a new node with `iex --sname foo`, giving `foo@bar`.

* `Node.self` returns the name of the current node.
* `Node.list` shows a list of currently connected nodes.
* `Node.connect` connects to another node.
