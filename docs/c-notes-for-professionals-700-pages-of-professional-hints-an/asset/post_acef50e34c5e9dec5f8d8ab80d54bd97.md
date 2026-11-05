
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

## Section 72.6: Operator nameof

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

Can be replaced with:

```csharp
string lengthName = nameof(string.Length);
```

The output will be Length in both examples. However, the latter prevents the creation of unnecessary instances.

Although the nameof operator works with most language constructs, there are some limitations. For example, you cannot use the nameof operator on open generic types or method return values:

```csharp
public static int Main()
{
    Console.WriteLine(nameof(List<>)); // Compile-time error
    Console.WriteLine(nameof(Main())); // Compile-time error
}
```

Furthermore, if you apply it to a generic type, the generic type parameter will be ignored:

```csharp
Console.WriteLine(nameof(List<int>)); // "List"
Console.WriteLine(nameof(List<bool>)); // "List"
```

For more examples, see this topic dedicated to nameof.

## Workaround for previous versions (more detail)

Although the nameof operator does not exist in C# for versions prior to 6.0, similar functionality can be had by using MemberExpression as in the following:

Version < 6.0

Expression:

```csharp
public static string NameOf<T>(Expression<Func<T>> propExp)
{
    var memberExpression = propExp.Body as MemberExpression;
    return memberExpression != null ? memberExpression.Member.Name : null;
}

public static string NameOf<TObj, T>(Expression<Func<TObj, T>> propExp)
{
    var memberExpression = propExp.Body as MemberExpression;
    return memberExpression != null ? memberExpression.Member.Name : null;
}
```

Usage:

```csharp
string variableName = NameOf(() => variable);
string propertyName = NameOf((Foo o) => o.Bar);
```

Note that this approach causes an expression tree to be created on every call, so the performance is much worse compared to nameof operator which is evaluated at compile time and has zero overhead at runtime.

## Section 72.7: Using static type

The using static [Namespace.Type] directive allows the importing of static members of types and enumeration values. Extension methods are imported as extension methods (from just one type), not into top-level scope.

Version ≥ 6.0

```csharp
using static System.Console;
using static System.ConsoleColor;
using static System.Math;

class Program
{
    static void Main()
    {
        BackgroundColor = DarkBlue;
        WriteLine(Sqrt(2));
    }
}
```

Live Demo Fiddle

Version < 6.0

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.BackgroundColor = ConsoleColor.DarkBlue;
        Console.WriteLine(Math.Sqrt(2));
    }
}
```

## Section 72.8: Index initializers

Index initializers make it possible to create and initialize objects with indexes at the same time.

This makes initializing Dictionaries very easy:

```csharp
var dict = new Dictionary<string, int>()
{
    ["foo"] = 34,
    ["bar"] = 42
};
```

Any object that has an indexed getter or setter can be used with this syntax:

```csharp
class Program
{
    public class MyClassWithIndexer
    {
        public int this[string index]
        {
            set
            {
                Console.WriteLine($"Index: {index}, value: {value}");
            }
        }
    }
}
```

```
public static void Main()
{
    var x = new MyClassWithIndexer()
    {
        ["foo"] = 34,
        ["bar"] = 42
    };
    Console.ReadKey();
}
```

Output:

Index: foo, value: 34
Index: bar, value: 42

View Demo

If the class has multiple indexers it is possible to assign them all in a single group of statements:

```
class Program
{
    public class MyClassWithIndexer
    {
        public int this[string index]
        {
            set
            {
                Console.WriteLine($"Index: {index}, value: {value}");
            }
        }
        public string this[int index]
        {
            set
            {
                Console.WriteLine($"Index: {index}, value: {value}");
            }
        }
    }

    public static void Main()
    {
        var x = new MyClassWithIndexer()
        {
            ["foo"] = 34,
            ["bar"] = 42,
            [10] = "Ten",
            [42] = "Meaning of life"
        };
    }
}
```

Output:

Index: foo, value: 34
Index: bar, value: 42
Index: 10, value: Ten
Index: 42, value: Meaning of life

It should be noted that the indexer set accessor might behave differently compared to an Add method (used in collection initializers).

For example:

```
var d = new Dictionary<string, int>
{
    ["foo"] = 34,
    ["foo"] = 42,
}; // does not throw, second value overwrites the first one
```

versus:

```
var d = new Dictionary<string, int>
{
    { "foo", 34 },
    { "foo", 42 },
}; // run-time ArgumentException: An item with the same key has already been added.
```

## Section 72.9: Improved overload resolution

Following snippet shows an example of passing a method group (as opposed to a lambda) when a delegate is expected. Overload resolution will now resolve this instead of raising an ambiguous overload error due to the ability of C# 6 to check the return type of the method that was passed.

```
using System;
public class Program
{
    public static void Main()
    {
        Overloaded(DoSomething);
    }

    static void Overloaded(Action action)
    {
        Console.WriteLine("overload with action called");
    }

    static void Overloaded(Func<int> function)
    {
        Console.WriteLine("overload with Func<int> called");
    }

    static int DoSomething()
    {
        Console.WriteLine(0);
        return 0;
    }
}
```

Results:

Version = 6.0

### Output

> overload with Func<int> called

View Demo

Version = 5.0

### Error

> error CS0121: The call is ambiguous between the following methods or properties: 'Program.Overloaded(System.Action)' and 'Program.Overloaded(System.Func)'

C# 6 can also handle well the following case of exact matching for lambda expressions which would have resulted in an error in C# 5.

```csharp
using System;

class Program
{
    static void Foo(Func<Func<long>> func) {}
    static void Foo(Func<Func<int>> func) {}

    static void Main()
    {
        Foo(() => () => 7);
    }
}
```

## Section 72.10: Await in catch and finally

It is possible to use await expression to apply await operator to Tasks or Task(Of TResult) in the catch and finally blocks in C#6.

It was not possible to use the await expression in the catch and finally blocks in earlier versions due to compiler limitations. C#6 makes awaiting async tasks a lot easier by allowing the await expression.

```csharp
try
{
    //since C#5
    await service.InitializeAsync();
}
catch (Exception e)
{
    //since C#6
    await logger.LogAsync(e);
}
finally
{
    //since C#6
    await service.CloseAsync();
}
```

It was required in C# 5 to use a bool or declare an Exception outside the try catch to perform async operations.
