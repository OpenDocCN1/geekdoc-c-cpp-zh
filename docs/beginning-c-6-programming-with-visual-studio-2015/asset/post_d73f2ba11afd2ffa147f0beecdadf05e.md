
```
}
}
WriteLine();
}
```

In the Main() method you create three lambda expressions and use them to call PerformOperations() in turn. The first of these calls is as follows:

```
WriteLine($"(a, b) = a + b;");
PerformOperations((paramA, paramB) => paramA + paramB);
```

The lambda expression used here is as follows:

```
(paramA, paramB) => paramA + paramB
```

Again, this breaks down into three parts:

- 1. A parameter definition section. Here there are two parameters, paramA and paramB. These parameters are untyped, meaning the compiler can infer the types of these parameters according to the context. In this case the compiler can determine that the PerformOperations() method call requires a delegate of type TwoIntegerOperationDelegate. This delegate type has two int parameters, so by inference both paramA and paramB are typed as int variables.
- 2. The => operator. This separates the lambda expression parameters from the lambda expression body.
- 3. The expression body. This specifies a simple operation, which is the summation of paramA and paramB. Notice that there is no need to specify that this is a return value. The compiler knows that in order to create a method that can be used with TwoIntegerOperationDelegate, the method must have a return type of int. Because the operation specified, paramA + paramB, evaluates to an int, and no additional information is supplied, the compiler infers that the result of this expression should be the return type of the method.

In longhand then, you can expand the code that uses this lambda expression to the following code that uses an anonymous method:

```
WriteLine($"(a, b) = a + b;");
PerformOperations(delegate(int paramA, int paramB)
{
    return paramA + paramB;
});
```

The remaining code performs operations using two different lambda expressions in the same way:

```
WriteLine();
WriteLine($"(a, b) = a * b;");
PerformOperations((paramA, paramB) => paramA * paramB);
WriteLine();
WriteLine($"(a, b) = (a - b) % b;");
PerformOperations((paramA, paramB) => (paramA - paramB)
    % paramB);
ReadKey();
```

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

## Lambda Expressions and Collections

Now that you have learned about the Func<> generic delegate, you can understand some of the extension methods that the System.Linq namespace provides for array types (which you might have seen popping up in IntelliSense at various points during your coding). For example, there is an extension method called Aggregate(), which is defined with three overloads as follows:

```
public static TSource Aggregate<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, TSource, TSource> func);
public static TAccumulate Aggregate<TSource, TAccumulate>(
    this IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate, TSource, TAccumulate> func);
public static TResult Aggregate<TSource, TAccumulate, TResult>(
    this IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate, TSource, TAccumulate> func,
    Func<TAccumulate, TResult> resultSelector);
```

As with the extension method shown earlier, this looks at first glance to be impenetrable, but if you break it down you can work it out easily enough. The IntelliSense for this function tells you that it does the following:

> Applies an accumulator function over a sequence.

This means that an accumulator function (which you can supply in the form of a lambda expression) will be applied to each element in a collection from beginning to end. This accumulator function must have two parameters and one return value. One input is the current element; the other input is either a seed value, the first value in the collection, or the result of the previous evaluation.

In the simplest of the three overloads, there is only one generic type specification, which can be inferred from the type of the instance parameter. For example, in the following code the generic type specification will be int (the accumulator function is left blank for now):

```
int[] myIntArray = { 2, 6, 3 };
int result = myIntArray.Aggregate(...);
```

This is equivalent to the following:

```
int[] myIntArray = { 2, 6, 3 };
int result = myIntArray.Aggregate<int>(...);
```

The lambda expression that is required here can be deduced from the extension method specification. Because the type TSource is int in this code, you must supply a lambda expression for the delegate Func<int, int, int>. For example, you could use one you've seen before:

```
int[] myIntArray = { 2, 6, 3 };
int result = myIntArray.Aggregate((paramA, paramB) => paramA + paramB);
```

This call results in the lambda expression being called twice, first with paramA = 2 and paramB = 6, and once with paramA = 8 (the result of the first calculation) and paramB = 3. The final result

assigned to the variable result will be the int value 11 — the summation of all the elements in the array.

The other two overloads of the Aggregate() extension method are similar, but enable you to perform slightly more complicated processing. This is illustrated in the following short Try It Out.

## TRY IT OUT Using Lambda Expressions with Collections: Ch13Ex09\Program.cs

- 1. Create a new console application called Ch13Ex09 and save it in the directory C:\BegVCSharp\Chapter13.
- 2. Modify the code in Program.cs as follows:
- 3. Run the application. The result is shown in Figure 13-21.

```csharp
static void Main(string[] args)
{
    string[] curries = { "pathia", "jalfrezi", "korma" };
    WriteLine(curries.Aggregate(
        (a, b) => a + " " + b));
    WriteLine(curries.Aggregate<string, int>(
        0,
        (a, b) => a + b.Length));
    WriteLine(curries.Aggregate<string, string, string>(
        "Some curries: ",
        (a, b) => a + " " + b,
        a => a));
    WriteLine(curries.Aggregate<string, string, int>(
        "Some curries: ",
        (a, b) => a + " " + b,
        a => a.Length));
    ReadKey();
}
```

![](img/cf72ea860016d2d680fc085fc06f265a_427_0.png)

## How It Works

In this example you experimented with each of the overloads of the Aggregate() extension method, using a string array with three elements as source data.

First, a simple concatenation is performed:

```
WriteLine(curries.Aggregate((a, b) => a + " " + b));
```
