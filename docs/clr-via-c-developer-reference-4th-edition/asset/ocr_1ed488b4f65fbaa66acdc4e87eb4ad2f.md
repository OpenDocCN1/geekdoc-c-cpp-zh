// Calling extension method: NullReferenceException will NOT be thrown when calling IndexOf
// NullReferenceException will be thrown inside IndexOf's for loop
sb.IndexOf('X');

// Calling instance method: NullReferenceException WILL be thrown when calling Replace
sb.Replace('.', '!');

I'd like to point out that you can define extension methods for interface types, as the follow-
code shows.

```
public static void ShowItems<T>(this IEnumerable<T> collection) {
    foreach (var item in collection)
        Console.WriteLine(item);
}
```

The extension method above can be invoked using any expression that results in a type that
implements the IEnumerable<T> interface.

```
public static void Main() {
    // Shows Char on a separate line in the console
    "Grant".ShowItems();

    // Shows String on a separate line in the console
    new[] { "Jeff", "Kristin" }.ShowItems();

    // Shows Int32 value on a separate line in the console
    new List<Int32>{ 1, 2, 3 }.ShowItems();
}
```

> Important extension methods are the cornerstone of Microsoft's Language Integrated
Query (LINQ) technology. For a great example of a class that offers many extension meth-\oods see the system. Linq.Enumerable class and all its static extension methods in
The Microsoft .NET Framework SDK documentation. Every extension method in this class
extxtends either the IEnumerable or IEnumerable<T> interface.

You can define extension methods for delegate types, too. Here is an example.

```
public static void InvokeAndCatch<TException>(this Action<Object> d, Object o)
where TException : Exception {
    try { d(o); }
    catch (TException) { }
}
```

And here is another example of how to invoke.

```
Action<Object> action = o => Console.WriteLine(o.GetType()); // Throws NullReferenceException
action.InvokeAndCatch<NullReferenceException>(null); // Swallows NullReferenceException
```

You can add extension methods to enumerated types. I show an example of this in the "Add-
ing Methods to Enumerated Types" section in Chapter 15, "Enumerated Types and Bit Flags."