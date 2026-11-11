Sequencing can also be used to generate lists and arrays, although in these cases the generation is not lazy. In fact, the primary difference between lists and sequences in F# is that sequences are lazy, and thus can be infinite, whereas lists are not lazy. Lists are in their entirety stored in memory. That is not the case with sequences.

The functions of F# are similar to those of ML and Haskell. If named, they are defined with `let` statements. If unnamed, which means technically they are lambda expressions, they are defined with the `fun` reserved word. The following lambda expression illustrates their syntax:

```
```fsharp
(fun a b -> a / b)
```
```

Note that there is no difference between a name defined with `let` and a function without parameters defined with `let`.

Indentation is used to show the extent of a function definition. For example, consider the following function definition:

```
```fsharp
let f =
    let pi = 3.14159
    let twoPi = 2.0 * pi
    twoPi;;
```
```

Note that F#, like ML, does not coerce numeric values, so if this function used 2 in the second-last line, rather than 2.0, an error would be reported.

If a function is recursive, the reserved word `rec` must precede its name in its definition. Following is an F# version of factorial:

```
```fsharp
let rec factorial x =
    if x <= 1 then 1
    else n * factorial(n - 1)
```
```

Names defined in functions can be outscoped, which means they can be redefined, which ends their former scope. For example, we could have the following:

```
```fsharp
let x4 x =
    let x = x * x
    let x = x * x
    x;;
```
```

In this function, the first `let` in the body of the x4 function creates a new version of x, defining it to have the value of the square of the parameter x. This terminates the scope of the parameter. So, the second `let` in the function body uses the new x in its right side and creates yet another version of x, thereby terminating the scope of the x created in the previous `let`.

There are two important functional operators in F#, pipeline (|>) and function composition (>>). The pipeline operator is a binary operator that