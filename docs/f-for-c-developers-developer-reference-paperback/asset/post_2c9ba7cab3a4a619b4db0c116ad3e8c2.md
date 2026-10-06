
```fsharp
seq { 0..100 }
///given data from 0 to 100
| Seq.filter checkOdd
///data subset contains only odd numbers
| Seq.sum
///sum them up
| printf("the sum of odd number from 0 to 100 is %d") //print out the result
```

As the code is getting cleaner, somebody might notice the Seq.filter function takes a function as input. F# treats values and functions the same. If a function takes a function or returns a function, it is called a higher-order function. In Listing 1-67, Seq.filter is a higher-order function. The Seq.filter function provides the skeleton of a filter algorithm. You can then implement your special filter mechanism and pass your function into the skeleton function. Higher-order functions provide an extremely elegant way to reuse code. The higher-order function is a light-weight Strategy pattern.

We have finished our refactoring. You might already be eager to see the class definition in F#, before I start introducing how F# handles object-oriented concepts as classes, we need to spend a little more time on some basics.

## Recursive Functions

The keyword rec is needed when defining a recursive function. Listing 1-68 shows how to use the rec keyword to define a function to compute Fibonacci numbers.

LISTING 1-68 Using the rec keyword to define a recursive function

```fsharp
let rec fib n =
    if n < 2 then 1
    else fib (n - 1) + fib (n - 2)
```

> Note This recursive version does not use a tail call (which is defined later in this section), this version can generate a stack overflow error.

Sometimes a function is mutually recursive because the calls form a circle. Listing 1-69 shows the mutually recursive Even and Odd functions. The F# variable and function resolution is from top to bottom and from left to right. All the functions and variables must be declared first before they can be referenced. In this case, you have to use the and keyword to let the compiler know.

LISTING 1-69 Mutually recursive function definition

```fsharp
let rec Even x = //Even calls Odd
    if x = 0 then true
    elif x = 1 then false
    else Odd (x - 1)
and Odd x = //Odd calls Even
    if x = 1 then true
    elif x = 0 then false
    else Even (x - 1)
```

In C#, the stack overflow exception can happen when you use a recursive function. A small amount of memory is allocated when doing each recursive function call, and tail allocation can lead to a stack overflow exception when a large amount of recursion is needed. A tail call is a function whose result is immediately treated as the output of the function. Thanks to the tail call in F#, the F# compiler generates a tail-call instruction to eliminate the stack overflow problem when possible. Figure 1-15 shows the project setting's Build tab, where you can select (or deselect) the Tail Calls check box.

| Application | Configuration: Active (Debug) | Platform: Active (Any CPU) |
|---|---|---|
| Build | General | |
| Build Events | Conditional compilation symbols: [x] DEFINE DEBUG constant [x] DEFINE TRACE constant | Platform target: [ Any CPU ] |
| | Other flags: [ ] Prefer 32-bit [ ] Optimize code [ ] Generate tail calls | |

FIGURE 1-15 The Generate Tail Calls check box on the project setting's Build tab

## Pipe/Composite Operators

Because functional programming languages see no difference between data and functions, you might be wondering if there are any operators specifically for functions. The pipe-forward operator was introduced already. The real function operators are forward and backward composite operators. See Listing 1-70.

## LISTING 1-70 Composing two functions into a new function using the forward composite operator

```fsharp
let f0 x = x * 2
let f1 x = x + 7
//composite f and g to get a new function
// g(x) = x + 11
// the f0 function is executed first and then f1
let g = f0 >> f1
// result is 2*2+7 = 11
let result = g 2
```

The forward composite operator executes the function from the left to right. The backward composition operator executes the function in the opposite direction, from right to left. Listing 1-71 demonstrates these operators.

## LISTING 1-71 Composing two functions into a new function using the backward composite operator

```fsharp
let f0 x = x * 2
let f1 x = x + 7
// composite f and g to get a new function
// g(x) = x + 11
// the f1 function is executed first and then f0
let g = f0 << f1

// result is (2+7)*2 = 18
let result = g 2
```

Similar to the backward composite operator, F# also has a backward pipe operator (<|). The backward pipe operator uses left associativity. The code f|< g <| x is parsed as (f <| g) <| x. It is not parsed as f <| (g <| x), which is equivalent to x | f. See Listing 1-72.

## LISTING 1-72 Comparing forward and backward pipe operators

```fsharp
Pipe-forward operator
let f x = x * 2
let g x = x + 5
// forwardPipeResult is 3*2 + 5 = 11
let forwardPipeResult = 3 |> f |> g
```

## Pipe-forward operator

```fsharp
let f x = x * 2
let g x = x + 5
// forwardPipeResult is 3*2 + 5 = 11
let forwardPipeResult = 3 |> f |> g
```

## Pipe-backward operator

```fsharp
let f x = x * 2
let g x = x + 5
// forwardPipeResult is 3*2 + 5 = 11
let forwardPipeResult = 3 |> f |> g
```

## Unit Types

If a C# method does not have a return value, use void to tell the compiler. In F#, the unit keyword is used to accomplish this. There are two ways to tell the compiler that a function returns unit:

- Specify the return type in the function. See Listing 1-75.

LISTING 1-75 A function with return type unit

```fsharp
//define a return type unit
let f (x) : unit = ()

//define a function with int parameter and unit type
let f (x:int) : unit = ()
```

- Make the () be the last statement. As I mentioned earlier in this chapter, F# functions do not use the return keyword. Instead, F# takes the type from the last statement that the function returns. So the following functions returns unit as well. You can use the ignore operator to throw the result, which makes the function return nothing.

```fsharp
// define a function returns unit
let f x = () // f : 'a -> unit
```

```fsharp
// use ignore to throw away the keyboard input and f2 returns unit
let f2 ( ) = System.Console.ReadLine() |> ignore
```

> > **Note** When a function can be passed in as a parameter to another function, the passed-in function is of type Microsoft.Fsharp.Core.FsharpFunc. The function, which is passed in as a parameter, can be called by calling the Microsoft.Fsharp.Core.FsharpFunc.Invoke method. When this is the case, the Invoke of a function returning unit actually returns the Microsoft.Fsharp.Core.Unit type, which is not valid at all. Fortunately, the F# Compiler handles this so that you do not have to be aware of the subtle difference when coding.

## Type Aliases

Another nice F# feature allows you to give a type alias. Listing 1-76 shows how to give the built-in system type a different name. This feature is more typedef in C++. From the execution result, you can see that the int type can now be referenced using I.

LISTING 1-76 A type alias and the FSI execution result

```fsharp
type I = int
let f (a:I) = a + i;

type I = int
val f : I -> ignore
```
