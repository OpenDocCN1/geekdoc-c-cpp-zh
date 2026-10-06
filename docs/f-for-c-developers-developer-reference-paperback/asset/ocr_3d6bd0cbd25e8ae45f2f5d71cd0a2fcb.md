The Gli function is a powerful weapon you can use to crack the boundary of encapsulation formed by a class. It requires only that the signature of the methods match. If you ponder this feature, you can see how this could be something significant. And you are right. The Gli function is the fundamental building block for one of our design patterns that was discussed in Chapter 3. The other application is to use this function in the library with the `inline` keyword, which will be discussed in the next section.

# Using the inline function

The `inline` keyword changes the type resolution. Listing 6-72 shows how to use the `inline` keyword to change variable x's inferred type to any type. This makes it that x can be a `float` as well as an `int`.

**LISTING 6-72** *The inline* keyword affects the type inferrence

```
let F = float x + 1.0
let inline F_inline x = float x + 1.0

Execution result in FSI

val F : int -> float
val inline F_inline : ^a : (static member op_Explicit : ^a -> float)
```

The `inline` keyword can be applied to functions at the top level, at the module level, or to the method in the class. See Listing 6-73.

**LISTING 6-73** *The inline* keyword

```
let inline f x = x + 1
type InlineSample() =
  member inline this.F x = x + 1
  static inline F x = x + 1
```

The `inline` keyword optimizes the code, but this should be the last item on your optimization to-do list.