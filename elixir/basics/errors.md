# Errors

Used only for things that are exceptional. Some keywords for handling errors:

* `raise`
* `try`
* `rescue`
* `throw`
* `catch`
* `after`

```elixir
raise "problem"
#=> ** (RuntimeError) problem

defmodule MyError do
  defexception message: "default message"
end

raise MyError
#=> ** (MyError) default message
raise MyError, message: "custom message"
#=> ** (MyError) custom message

try do
  raise "problem"
rescue
  RuntimeError -> "Error!"
end
#=> "Error!"
```
