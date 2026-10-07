# TABLE 13.1: Lambda Expression Notes, Errors, and Examples (continued)

| Statement | Example |
| --- | --- |
| | int number; Func<int, bool> isFortyTwo = x >= 42 == (number = x); if (isFortyTwo(42)) { // ERROR: Use of unassigned local variable Console.Write(number); } |

# Anonymous Methods

An anonymous method is like a statement lambda,¹¹⁰ but without many of the features that make lambdas so compact. An anonymous method must explicitly type every parameter, and it must have a statement block. Rather than using the lambda operator => between the parameter list and the code block, an anonymous method puts the keyword delegate before the parameter list, emphasizing that the anonymous method must be converted to a delegate type. Listing 13.17 shows the code from Listing 13.7, Listing 13.12, and Listing 13.15 rewritten to use an anonymous method.

# LISTING 13.17: Passing an Anonymous Method in C# 2.0

```
//...
DelegateSample.BubbleSort(items,
    delegate(int first, int second)
{
    return first < second;
}
);////...
```

Anonymous methods support one small feature that is not supported in lambda expressions: Anonymous methods may omit their parameter list entirely in their circumstances.

10. Lambda expressions were not yet available in C# 2.0.