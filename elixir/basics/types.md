# Types

## Integer

Integers can be decimal `1234`, hexadecimal `0xcafe`, octal `0o765` and binary `0b1010`. Commas are not allowed in numbers, but underscores are. So if you feel the need to mark your thousands so the numbers are more readable, use an underscore, as in `12_000_000_000`.

## Float

Floats consist of numbers with a decimal place or scientific notation. `3.14`, `-808.08` and `12.043e-04` are examples. Maximum value of around `1.0e308`.

## Atom

Atoms are words that look just like variables, starting with a colon, like `:true` or even `:"chunky bacon"`. An atom’s name is its value and two atoms with the same name will always compare as being equal. In fact, the booleans `true` and `false` (and `nil`!) are in fact atoms:

```elixir
false == :false #=> true
```

[Erlang modules](http://elixir-lang.org/getting-started/erlang-libraries.html) are accessible using atoms, like `:io.format`. All module names are in fact atoms. Elixir modules like `Enum` are really `:Elixir.Enum`. Module names start with a capital letter and are [aliased](modules.html#alias) like that.

Atoms are never garbage collected and should never be converted from user input. The Erlang VM has a limit for the number of atoms that can be created.

## Range

A range is two integers separated by two dots like so: `1..5`. Can be increasing or decreasing and are represented internally as a [struct](#structs) with fields `:first` and `:last`.

## Regex

A regular expression can be created with the [sigil](#sigils) `~r{regex}opts` and are represented internally as a [struct](#struct).

[Reference for Regex](https://hexdocs.pm/elixir/Regex.html) and [Elixir regular expression editor & tester](http://www.elixre.uk/).

# Collections

Collection functions use this rule to define its complexity:

* Size – constant time (pre-calculated)
* Length – linear (slower as input grows)

## Tuple

Tuples is an ordered collection of values, defined by curly brackets.

```elixir
{:ok, "hello"}
```

Tuples are stored contiguously in memory: getting the tuple size or accessing an element is fast, however adding or updating elements is expensive – because of immutability, the whole tuple needs to be copied in memory.

```elixir
# Kernel functions for working with tuples
elem/2, put_elem/3, tuple_size/1
```

**Records** are tuples where the first element is an atom, they are related to Erlang records.

## List

Lists are collection of values, defined by square brackets. The **cons operator** can be used to construct lists, separating its head from its tail.

```elixir
[1, 2, :hello]
# is the same as:
[ 1 | [ 2 | [ :hello | [] ] ] ]
```

Lists are stored in memory as linked lists: accessing the length of a list is a linear operation (traversing the whole list is necessary). Updating a list is fast as long as you are prepending elements.

```elixir
# Kernel functions for working with lists
++/2, --/2, length/1, hd/1, tl/1
```

## Keyword lists

A keyword list is a list of two element tuples. It is often used for options as the last argument of a function, where you can drop all of the braces.

```elixir
[{:one, 1}, {:two, 2}, {:three, 3}]
# can also be written as:
[one: 1, two: 2, three: 3]
```

* More than one of the same key
* Guarantees elements are ordered
* Keys must be atoms

## Map

Maps are key-value stores, created using the `%{}` syntax. Map keys don't follow any ordering.

```elixir
map = %{:a => 1, 5 => "work"} #=> %{5 => "work", :a => 1}
map[:a] #=> 1

user = %{name: "John", age: 27}

# Strict access
user.age #=> 27
user.address
# ** (KeyError) key :address not found in: %{age: 27, name: "John"}

# Dynamic access
user[:age] #=> 27
user[:address] #=> nil

# updating values
older_john = %{user | age: 28} #=> %{age: 28, name: "John"}
```

* Only one of the same key
* Keys can be of any type
* Useful when pattern matching and for many items

```elixir
# Kernel functions and macros for working with nested maps
get_and_update_in/2, get_in/2, map_size/1 put_in/2, update_in/2
```

### Structs

Structs are modules that define custom maps with specific keys and default values, and only those keys are allowed. Structs are maps with a `__struct__` key holding the name of its module. They don't implement the Access or Enumerable protocol.

```elixir
defmodule User do
  defstruct [name: "John", age: 27]
end

john = %User{} #=> %User{age: 27, name: "John"}
meg = %User{name: "Megan"} #=> %User{name: "Megan", age: 27}

inspect(john, structs: false)
#=> "%{__struct__: User, age: 27, name: \"John\"}"

# Strict access only
meg.name #=> "Megan"

john[:name]
# ** (UndefinedFunctionError) function User.fetch/2 is undefined
# (User does not implement the Access behaviour)
#              User.fetch(%User{age: 27, name: "John"}, :name)
```

Using `@enforce_keys` makes the keys mandatory when creating a new struct.

```elixir
defmodule User do
  @enforce_keys [:name]
  defstruct [name: "John", age: 27]
end

john = %User{}
# ** (ArgumentError) the following keys must also be given when
# building struct User: [:name]
#    expanding struct: User.__struct__/1
```

## Binary

Binaries are sequence of bytes enclosed by `<< >>` and separated with `,`.

```elixir
# Kernel functions for working with binaries
binary_part/3, bit_size/1, byte_size/1, is_binary/1, is_bitstring/1
```

### Strings

Strings are binaries encoded in UTF-8 and are represented as `"chunky bacon"`. String interpolation is supported with `#{}`. A codepoint is a single Unicode character, represented by one or more bytes. A grapheme may consist of multiple codepoints but are perceived as a single character by the reader.

Escape sequences:

* `\"` – double quote
* `\'` – single quote
* `\\` – single backslash
* `\a` – bell/alert
* `\b` – backspace
* `\d` - delete
* `\e` - escape
* `\f` - form feed
* `\n` – newline
* `\r` – carriage return
* `\s` – space
* `\t` – tab
* `\v` – vertical tab
* `\0` - null byte
* `\xDD` - represents a single byte in hexadecimal (such as `\x13`)
* `\uDDDD` and `\u{D...}` - represents a Unicode codepoint in hexadecimal (such as `\u{1F600}`)

### Sigils

Sigils are alternative syntax for working with textual representation.

```elixir
~s{hello dogs and cats} #=> "hello dogs and cats"
~w{dog cat}             #=> ["dog", "cat"]
```

| Default sigils ids  | Description                                          |
| :-----------------  | :--------------------------------------------------  |
| c                   | character list without escaping or interpolation     |
| C                   | character list with escaping and interpolation       |
| D                   | dates                                                |
| N                   | naive date times                                     |
| r                   | regular expression without escaping or interpolation |
| R                   | regular expression with escaping and interpolation   |
| s                   | string without escaping or interpolation             |
| S                   | string with escaping and interpolation               |
| T                   | times                                                |
| w                   | word lists without escaping or interpolation         |
| W                   | word lists with escaping and interpolation           |

It is possible to define you own sigil by creating a function `sigil_[id]`. Sigils are accessible in the module they are defined and other modules that import it.

```elixir
def sigil_i(string, []), do: String.to_integer(string)
```
