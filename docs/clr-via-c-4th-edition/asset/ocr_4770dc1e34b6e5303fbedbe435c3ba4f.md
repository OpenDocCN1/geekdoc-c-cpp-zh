```
// Calling extension method: NullReferenceException will NOT be thrown when calling IndexOf
// NullReferenceException will be thrown inside IndexOf's for loop
sb.IndexOf('X');

// Calling instance method: NullReferenceException WILL be thrown when calling Replace
sb.Replace('.', '!');
```

I’d also like to point out that you can define extension methods for interface types, as the following code shows.

```
public static void ShowItems<T>(this IEnumerable<T> collection) {
    foreach (var item in collection)
        Console.WriteLine(item);
}
```

The extension method above can now be invoked using any expression that results in a type that implements the IEnumerable<T> interface.

```
public static void Main() {
    // Shows each Char on a separate line in the console
    "Grant".ShowItems();

    // Shows each String on a separate line in the console
    new[] { "Jeff", "Kristin" }.ShowItems();

    // Shows each Int32 value on a separate line in the console
    new List<Int32>() { 1, 2, 3 }.ShowItems();
}
```

> > **Important** Extension methods are the cornerstone of Microsoft’s Language Integrated Query (LINQ) technology. For a great example of a class that offers many extension methods, see the static System.Linq.Enumerable class and all its static extension methods in the Microsoft .NET Framework SDK documentation. Every extension method in this class extends either the IEnumerable or IEnumerable<T> interface.

You can define extension methods for delegate types, too. Here is an example.

```
public static void InvokeAndCatch<TException>(this Action<Object> d, Object o)
    where TException : Exception {
    try { d(o); }
    catch (TException) { }
}
```

And here is an example of how to invoke it.

```
Action<Object> action = o => Console.WriteLine(o.GetType()); // Throws NullReferenceException
action.InvokeAndCatch<NullReferenceException>(null);          // Swallows NullReferenceException
```

You can also add extension methods to enumerated types. I show an example of this in the “Adding Methods to Enumerated Types” section in Chapter 15, “Enumerated Types and Bit Flags.”