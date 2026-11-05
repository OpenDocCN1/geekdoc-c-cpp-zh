```
IEnumerable<string> Digits => Enumerable.Range(0, 10).Select(i => i.ToString());
```

In all other cases, the old syntax for function members can be used.

Expression-bodied function members can contain async/await, but it's often redundant:

```
async Task<int> Foo() => await Bar();
```

Can be replaced with:

```
Task<int> Foo() => Bar();
```

# Section 72.6: Operator nameof

The nameof operator returns the name of a code element as a string. This is useful when throwing exceptions related to method arguments and also when implementing INotifyPropertyChanged.

```
public string SayHello(string greeted)
{
    if (greeted == null)
        throw new ArgumentNullException(nameof(greeted));
    Console.WriteLine("Hello, " + greeted);
}
```

The nameof operator is evaluated at compile time and changes the expression into a string literal. This is also useful for strings that are named after their member that exposes them. Consider the following:

```
public static class Strings
{
    public const string Foo = nameof(Foo); // Rather than Foo = "Foo"
    public const string Bar = nameof(Bar); // Rather than Bar = "Bar"
}
```

Since nameof expressions are compile-time constants, they can be used in attributes, case labels, switch statements, and so on.

It is convenient to use nameof with Enums. Instead of:

```
Console.WriteLine(Enum.One.ToString());
```

it is possible to use:

```
Console.WriteLine(nameof(Enum.One))
```

The output will be One in both cases.

The nameof operator can access non-static members using static-like syntax. Instead of doing:

```
string foo = "Foo";
string lengthName = nameof(foo.Length);
```