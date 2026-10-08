```
| Number n ->
cont n
| Binop (f, e1, e2) ->
Eval (fun i1 ->
Eval e2 (fun i2 ->
 f i1 i2 | cont))
```

The Eval function receives an expression and an explicit continuation that takes the result of the expression. When the expression is a number, you simply pass it to the continuation. If the expression is a binary operation, you evaluate the first operand with a continuation function that evaluates the second operand, which itself gets a continuation that takes both of the evaluated results, applies the binary operation on them, and passes the overall result to the original continuation.

CPS is a common functional pattern, used for translating between different representations or traversing data types.

# Using Tuples

Tuples are a fundamental functional data structure, another wellknown of F# development. They are a versatile data type that .NET 4.0 finally included them as a system type as System.Tuple, pioneered and inspired by F#.

Tuples are also referred to as product types, because they constitute the Cartesian product of their parts, and also because, in theory, they are denoted by a star symbol (such as T1*T2*T3). As you saw earlier, in F# type signatures, tuples are marked with the star symbol (such as T1*T2*T3).

You can construct tuples by connecting values with a comma:

+   1, "my string", 3

Often, you must parenthesize to avoid precedence errors — for example, when you call a function that takes a tuple, argument, as you saw in the beginning of this chapter:

```
(1, "my string", 3) | MyFunction
```

Here, the function call (or the pipe operator) has higher precedence than a comma, and without parentheses, it would only apply to the value in the intended tuple.

Tuples are also called n-tuples for any n, where the tuple groups n separate values together. You can nest tuples in tuples, so the following are different values:

```
(1, "my string", 3)
(1, ("my string", 3))
((1, "my string"), 3)
```

You can use pattern matching to deconstruct tuples, as you will see later in this chapter. F# also provides some utility functions to work with pairs:

```
> fst (1, 2);
val it : int = 1
> snd (1, 2);
val it : int = 2
```