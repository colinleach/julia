# Introduction

A vector in Julia is a one-dimensional array with all elements of the same type. 

```julia-repl
julia> nums = [1, 2, 3]
3-element Vector{Int64}:
 1
 2
 3

julia> [1, 2.0, 3]
3-element Vector{Float64}:
 1.0
 2.0
 3.0
```

## Indexing

~~~~exercism/caution
Indexing is 1-based by default.

This is normal for scientific languages (Fortran, Matlab, etc) but differs from the zero-based indexing of system languages like C.
~~~~

```julia-repl
julia> nums = [1, 2, 3];

julia> nums[1]
1

julia> nums[0]
ERROR: BoundsError: attempt to access 3-element Vector{Int64} at index [0]

julia> nums[begin] # same as nums[1]
1

julia> nums[end] # last element
3

julia> nums[end-1]
2
```

Index ranges use a `:` separator

```julia-repl
julia> nums[2:3]
2-element Vector{Int64}:
 2
 3
```

## Manipulation

A wide range of functions is available, such as `push!()`, `pop!()` and `deleteat!()`. 
Many are broadly applicable to Julia collections, not just vectors: this affects how they are documented. 
See the [Julia docs](https://docs.julialang.org/en/v1/base/collections/) for full details, or [tutorialspoint](https://www.tutorialspoint.com/julia/julia_arrays.htm) for an introduction that may be more beginner-friendly.

~~~~exercism/caution
Be careful when googling these functions.
It is still easy to find references to `shift!()` and `unshift()`, which were in an early pre-1.0 version. They were renamed several years ago to `popfirst()` and `pushfirst()`.
