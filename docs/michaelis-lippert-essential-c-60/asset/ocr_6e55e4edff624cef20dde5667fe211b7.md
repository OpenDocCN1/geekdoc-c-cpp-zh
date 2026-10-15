The return type is missing, but the compiler can see that the lambda expression is being converted to a delegate whose signature requires the return type bool. The compiler verifies that the expressions of every return statement in the statement lambda’s block would be legal in a bool-returning method. The public modifier is missing; given that the method is no longer an accessible member of the containing class, there is no need to describe its accessibility. Similarly, the static modifier is no longer necessary. The amount of “ceremony” around the method is already greatly reduced.

The syntax is still needlessly verbose, however. We have deduced from the delegate type that the lambda expression must be bool-returning; we can similarly deduce that both parameters must be of type int, as shown in Listing 12.12.

# LISTING 12.12: Omitting Parameter Types from Statement Lambdas

```
// ...

BubbleSort(items,
    (first, second) =>
    {
        return first < second;
    }
);

// ...
```

In general, explicitly declared parameter types are optional in all lambda expressions if the compiler can infer the types from the delegate that the lambda expression is being converted to. For situations when specifying the type makes code more readable, however, C# enables you to do so. In cases where inference is not possible, the C# language requires that the lambda parameter types be stated explicitly. If one lambda parameter type is specified explicitly, then all of them must be specified explicitly, and they must all match the delegate parameter types exactly.

# Guidelines

CONSIDER omitting the types from lambda formal parameter lists when the types are obvious to the reader, or when they are an insignificant detail.