```
```csharp
Expression convertedRight = rightOperand;
if (typeof(T2) != typeof(TResult))
{
    convertedRight = Expression.Convert(rightOperand,
        typeof(TResult));
}
var body = Expression.Add(convertedLeft, convertedRight);
var adder = Expression.Lambda<Func<T1, T2, TResult>>(
    body, leftOperand, rightOperand);
return adder.Compile()(left, right);
}
```
```

That will fix all the problems with any addition that needs a conversion, like adding doubles and ints, or adding a double to string with the result being a string. However, it breaks valid usages where the parameters should not be the same as the result. In particular, this version would not work with the example above adding a TimeSpan to a DateTime. With a lot more code, you could solve this. However, at that point, you’ve pretty much reimplemented the code that handles dynamic dispatch for C# (see Item 41). Instead of all that work, just use dynamic.

You should use the expression version for those times when the operands and the result are the same. That gives you generic type parameter inference and fewer permutations when the code fails at runtime. Here’s the version I would recommend to use Expression for implementing runtime dispatch:

```
```csharp
public static class BinaryOperators<T>
{
    static Func<T, T, T> compiledExpression;

    public static T Add(T left, T right)
    {
        if (compiledExpression == null)
            createFunc();

        return compiledExpression(left, right);
    }

    private static void createFunc()
    {
        var leftOperand = Expression.Parameter(typeof(T),
            "left");
```
```