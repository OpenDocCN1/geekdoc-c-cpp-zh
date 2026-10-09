Notice that because the `IDisposable` interface is supported by `IEnumerator<T>`, the `using` statement can simplify the code in Listing 15.7 to that shown in Listing 15.8.

# **LISTING 15.8: Error Handling and Resource Cleanup with using**

```
```csharp
System.Collections.Generic.Stack<int> stack =
new System.Collections.Generic.Stack<int>();
int number;

using(
System.Collections.Generic.Stack<int>.Enumerator enumerator = stack.GetEnumerator())
{
while (enumerator.MoveNext())
{
number = enumerator.Current;
Console.WriteLine(number);
}
}
```
```

However, recall that the CIL does not directly support the `using` keyword. Thus the code in Listing 15.7 is actually a more accurate C# representation of the `foreach` CIL code.

# **ADVANCED TOPIC**

# **foreach without IEnumerable**

C# doesn't require that `IEnumerable`/`IEnumerable<T>` be implemented to iterate over a data type using `foreach`. Rather, the compiler uses a concept known as **duck typing**; it looks for a `GetEnumerator()` method that returns a type with a `Current` property and `MoveNext()` method. Duck typing involves searching by name rather than relying on an interface or explicit method call to the method. (The name “duck typing” comes from the whimsical idea that to be treated as a duck, the object must merely implement a `Quack()` method; it need not implement an `IDuck` interface.) If duck typing fails to find a suitable implementation of the enumerable pattern, the compiler checks whether the collection implements the interfaces.