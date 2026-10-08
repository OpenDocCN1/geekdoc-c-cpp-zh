# LISTING 25-1 (continued)

```
printf("Failure: %s" msg
System.Double.NaN
? System.DivideByZeroException -> // Pattern matching over
                                // types
printf("Error: division by zero")
System.Double.NaN
 =
[ 1; 4; 6; 8; 12; 15 ]
|> SillyComputation
|> printf("The result is=%f")
```

Several things would stand out if you are a C# or VB programmer (with many more standing out as you explore the content of this chapter):

+   - Indentation matters. The bodies of if-then-else blocks do not need to be enclosed in braces or between begin-end pairs. They are inferred the indentation level.
- There are a series of let bindings that bind to names, creating "variables" and "functions."
- The bindings you create do not change; there is no mutation. You can, of course, create bindings that can be updated, but require extra notation and, thus, easier to isolate.
- You can nest bindings, which creates nested local functions and bindings that are only visible in their scope.
- Functions are called without parentheses, and these calls are often chained together with |.
- There is no main function that triggers the execution. If you run the code in Listing 25-1 in F# Interactive, or if you compile it as a standalone program, it will print the result. The toplevel binding is discarded (via the underscore) the execution, and you may have multiple blocks, in multiple files.
- Thus, any value binding will trigger the evaluation of the value being bound, and all function bindings will postpone evaluation until the function is called, as you would expect.

# Understanding Functions and Pipel

Functional programming gets its name from one of its fundamental pillars: functions, the workhorses of F# development. In F#, functions can do the following:

+   - Appear over-the-fly other values (they are first-class values)
- Be created on (anonymous functions)
- Carry their closures
- Be passed to as arguments, or returned from other functions (higher-order functions)

As you will see in this chapter, functions are a powerful abstraction that can change the way you think about problems and their solutions.