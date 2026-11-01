An earlier example showed how a delegate with a void return type was less fussy about the code used in the statement body:

```
myTimer.Elapsed += (source, e) => WriteLine("Event handler called after " +
    $"{(source as Timer).Interval} milliseconds.");
```

Here, the statement doesn't evaluate to anything, so it is simply executed without any return value being used anywhere.

Given that lambda expressions can be visualized as an extension of the anonymous method syntax, you might not be surprised to learn that you can also include multiple statements as a lambda expression statement body. To do so, you simply provide a block of code enclosed in curly braces, much like any other situation in C# where you must supply multiple lines of code:

```
(param1, param2) =>
{
    // Multiple statements ahoy!
}
```

If you use a lambda expression in combination with a delegate type that has a non-void return type, then you must return a value with the return keyword, just like any other method:

```
(param1, param2) =>
{
    // Multiple statements ahoy!
    return returnValue;
}
```

For example, earlier you saw how you could rewrite the following code from the Try It Out,

```
PerformOperations((paramA, paramB) => paramA + paramB);
```

as:

```
PerformOperations(delegate(int paramA, int paramB)
{
    return paramA + paramB;
});
```

Alternatively, you could rewrite the code as follows:

```
PerformOperations((paramA, paramB) =>
{
    return paramA + paramB;
});
```

This is more in keeping with the original code because it maintains implicit typing of the paramA and paramB parameters.

For the most part, lambda expressions are at their most useful — and certainly their most elegant — when used with single expressions. To be honest, if you require multiple statements, your code