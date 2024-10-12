# About

## Pairs

A [`Pair`][pair] is just two items joined together.
The items are then imaginatively called `first` and `second`.

Create them either with the `=>` operator or the `Pair()` constructor.

```julia-repl
julia> p1 = "k" => 2
"k" => 2

julia> p2 = Pair("k", 2)
"k" => 2

# Both forms of syntax give the same result
julia> p1 == p2
true

# Each component has its own separate type
julia> dump(p1)
Pair{String, Int64}
  first: String "k"
  second: Int64 2

# Get a component using dot syntax
julia> p1.first
"k"

julia> p1.second
2
```

## Dicts

A `Vector` of Pairs is like any other array: ordered, homogeneous in type, and stored consecutively in memory.

```julia-repl
julia> pv = ['a' => 1, 'b' => 2, 'c' => 3]
3-element Vector{Pair{Char, Int64}}:
 'a' => 1
 'b' => 2
 'c' => 3

# Each pair is a single entry
julia> length(pv)
3
```

A [`Dict`][dict] is superficially similar, but storage is now implemented in a way that allows fast retrieval by key, known as a "hash table", even when the number of entries grows large.

```julia-repl
julia> pd = Dict(pv)
Dict{Char, Int64} with 3 entries:
  'a' => 1
  'c' => 3
  'b' => 2

julia> pd['b']
2

# Key must exist
julia> pd['d']
ERROR: KeyError: key 'd' not found

# Generators are accepted in the constructor (and note the unordered output)
julia> Dict(x => x^2 for x in 1:5)
julia> Dict(x => 1 / x for x in 1:5)
Dict{Int64, Float64} with 5 entries:
  5 => 0.2
  4 => 0.25
  2 => 0.5
  3 => 0.333333
  1 => 1.0
  ```

In other languages, something very similar to a `Dict` might be called a dictionary (Python), a Hash (Ruby) or a HashMap (Java).

For Pairs, whether in isolation or in a Vector, there are few constraints on the type of each component.

To be valid in a `Dict`, the `Pair` must be a `key => value` pair, where the `key` is "hashable".
Most importantly, this means the `key` must be _immutable_, so `Char`, `Int`, `String`, `Symbol`, and `Tuple` are all fine, but `Vector` is not allowed.

If mutable keys are important to you, there is a separate but much less common [`IdDict`][iddict] type that can allow this.
See the [manual][dict] for several other variants on the `Dict` type.

### Modifying a Dict

Entries can be added with a new key or overwritten with an existing key.

```julia-repl
# Add
julia> pd['d'] = 4
4

# Overwrite
julia> pd['a'] = 42
42

julia> pd
Dict{Char, Int64} with 4 entries:
  'a' => 42
  'c' => 3
  'd' => 4
  'b' => 2
```

To remove an entry, use the `delete!()` function, which will change the Dict if the key exists and silently do nothing otherwise.

```julia-repl
julia> delete!(pd, 'd')
Dict{Char, Int64} with 3 entries:
  'a' => 42
  'c' => 3
  'b' => 2
```

### Checking if a key or value exists

There are different approaches.
To check a key, there is a `haskey()` function:

```julia-repl
julia> haskey(pd, 'b')
true
```

Alternatively, search either the keys or the values:

```julia-repl
julia> 'b' in keys(pd)
true

julia> 43 in values(pd)
false

julia> 42 ∈ values(pd)
true
```

This remains efficient at scale, as the `keys()` and `values()` functions each return an iterator with a fast search algorithm.


[pair]: https://docs.julialang.org/en/v1/base/collections/#Core.Pair
[dict]: https://docs.julialang.org/en/v1/base/collections/#Dictionaries
[iddict]: https://docs.julialang.org/en/v1/base/collections/#Base.IdDict