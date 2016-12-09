# Tasks

Tasks are used to run a function asynchronously.

When invoking `Task.async/1,3` a new process will be created, linked and monitored by the caller. If no linking is desired, `Task.start/1,3` should be used.

The function `Task.await/2` is used to read the message sent by the task. The function `Task.shutdown/2` can be used to stop the task.

```elixir
task = Task.async(function)
res = Task.await(task)
```
