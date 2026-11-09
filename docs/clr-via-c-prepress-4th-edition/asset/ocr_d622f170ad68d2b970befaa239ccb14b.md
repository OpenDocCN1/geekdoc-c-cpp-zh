bind to Microsoft’s IndexOf instance method instead of my static IndexOf method. Because
of this, my program will experience different behavior. This versioning problem is another
reason why this feature should be used sparingly.

# # Extending Various Types with Extension Methods

In this chapter, I demonstrated how to define an extension method for a class, StringBuilder. I’d like
to point out that since an extension method is really the invocation of a static method, the CLR does
not emit code ensuring that the value of the expression used to invoke the method is not null:

```
```csharp
// sb is null
StringBuilder sb = null;

// Calling extension method: NullReferenceException will NOT be thrown when calling IndexOf
// NullReferenceException will be thrown inside IndexOf's for loop
sb.IndexOf('X');

// Calling instance method: NullReferenceException WILL be thrown when calling Replace
sb.Replace('.', '!');
```
```

I’d also like to point out that you can define extension methods for interface types as the following
code shows:

```
```csharp
public static void ShowItems<T>(this IEnumerable<T> collection) {
    foreach (var item in collection)
        Console.WriteLine(item);
}
```
```

The extension method above can now be invoked using any expression that results in a type that
implements the IEnumerable<T> interface:

```
```csharp
public static void Main() {
    // Shows each Char on a separate line in the console
    "Grant".ShowItems();

    // Shows each String on a separate line in the console
    new[] { "Jeff", "Kristin" }.ShowItems();

    // Shows each Int32 value on a separate line in the console
    new List<Int32>() { 1, 2, 3 }.ShowItems();
}
```
```

**Important** Extension methods are the cornerstone of Microsoft’s Language Integrated Query (LINQ)
technology. For a great example of a class that offers many extension methods, see the static
System.Linq.Enumerable class and all its static extension methods in the Microsoft .NET
Framework SDK documentation. Every extension method in this class extends either the
IEnumerable or IEnumerable<T> interface.

You can define extension methods for delegate types, too. Here is an example: