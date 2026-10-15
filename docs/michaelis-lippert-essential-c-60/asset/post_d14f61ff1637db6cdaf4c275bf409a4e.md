
The preceding example showed the gist of the C# compiler output, but it doesn’t actually compile that way because it omits two important details concerning the implementation: interleaving and error handling.

## State Is Shared

The problem with an implementation such as Listing 14.8 is that if two such loops interleaved each other—one foreach inside another, both using the same collection—the collection must maintain a state indicator of the current element so that when MoveNext() is called, the next element can be determined. In such a case, one interleaving loop can affect the other. (The same is true of loops executed by multiple threads.)

To overcome this problem, the collection classes do not support IEnumerator<T> and IEnumerator interfaces directly. As shown in Figure 14.1, there is a second interface, called IEnumerable<T>, whose only method is GetEnumerator(). The purpose of this method is to return an object that supports IEnumerator<T>. Instead of the collection class maintaining the state, a different class—usually a nested class, so that it has access to the internals of the collection—will support the IEnumerator<T> interface and will keep the state of the iteration loop. The enumerator is like a “cursor” or a “bookmark” in the sequence. You can have multiple bookmarks, and moving each of them enumerates over the collection independently of the other. Using this pattern, the C# equivalent of a foreach loop will look like the code shown in Listing 14.9.

### LISTING 14.9: A Separate Enumerator Maintaining State during an Iteration

```csharp
System.Collections.Generic.Stack<int> stack =
    new System.Collections.Generic.Stack<int>();
int number;
System.Collections.Generic.Stack<int>.Enumerator
    enumerator;

// ...

// If IEnumerable<T> is implemented explicitly,
// then a cast is required.
// ((IEnumerable<int>)stack).GetEnumerator();
enumerator = stack.GetEnumerator();
while (enumerator.MoveNext())
{
    number = enumerator.Current;
    Console.WriteLine(number);
}
```

## ADVANCED TOPIC

### Cleaning up Following Iteration

Given that the classes that implement the IEnumerator<T> interface maintain the state, sometimes you need to clean up the state after it exits the loop (because either all iterations have completed or an exception is thrown). To achieve this, the IEnumerator<T> interface derives from IDisposable. Enumerators that implement IEnumerator do not necessarily implement IDisposable, but if they do, Dispose() will be called as well. This enables the calling of Dispose() after the foreach loop exits. The C# equivalent of the final CIL code, therefore, looks like Listing 14.10.

### LISTING 14.10: Compiled Result of foreach on Collections

```csharp
System.Collections.Generic.Stack<int> stack =
    new System.Collections.Generic.Stack<int>();
System.Collections.Generic.Stack<int>.Enumerator
enumerator;
IDisposable disposable;

enumerator = stack.GetEnumerator();
try
{
    int number;
    while (enumerator.MoveNext())
    {
        number = enumerator.Current;
        Console.WriteLine(number);
    }
}
finally
{
    // Explicit cast used for IEnumerator<T>.
    disposable = (IDisposable) enumerator;
    disposable.Dispose();

    // IEnumerator will use the as operator unless IDisposable
    // support is known at compile time.
    // disposable = (enumerator as IDisposable);
    // if (disposable != null)
    // {
    //     disposable.Dispose();
    // }
}
```

Notice that because the IDisposable interface is supported by IEnumerator<T>, the using statement can simplify the code in Listing 14.10 to that shown in Listing 14.11.

### LISTING 14.11: Error Handling and Resource Cleanup with using

```csharp
System.Collections.Generic.Stack<int> stack =
    new System.Collections.Generic.Stack<int>();
int number;

using (
    System.Collections.Generic.Stack<int>.Enumerator
        enumerator = stack.GetEnumerator())
{
    while (enumerator.MoveNext())
    {
        number = enumerator.Current;
        Console.WriteLine(number);
    }
}
```

However, recall that the CIL does not directly support the using keyword. Thus the code in Listing 14.10 is actually a more accurate C# representation of the foreach CIL code.

## ADVANCED TOPIC

### foreach without IEnumerable

C# doesn’t require that IEnumerable/IEnumerable<T> be implemented to iterate over a data type using foreach. Rather, the compiler uses a concept known as **duck typing**; it looks for a GetEnumerator() method that returns a type with a Current property and MoveNext() method. Duck typing involves searching by name rather than relying on an interface or explicit method call to the method. (The name “duck typing” comes from the whimsical idea that to be treated as a duck, the object must merely implement a Quack() method; it need not implement an IDuck interface.) If duck typing fails to find a suitable implementation of the enumerable pattern, the compiler checks whether the collection implements the interfaces.

## Do Not Modify Collections during foreach Iteration

Chapter 3 showed that the compiler prevents assignment of the foreach variable (number). As is demonstrated in Listing 14.10, an assignment to number would not be a change to the collection element itself, so the C# compiler prevents such an assignment altogether.

In addition, neither the element count within a collection nor the items themselves can generally be modified during the execution of a foreach loop. If, for example, you called stack.Push(42) inside the foreach loop, it would be ambiguous whether the iterator should ignore or incorporate the change to stack—in other words, whether iterator should iterate over the newly added item or ignore it and assume the same state as when it was instantiated.

Because of this ambiguity, an exception of type System.InvalidOperationException is generally thrown upon accessing the enumerator if the collection is modified within a foreach loop, reporting that the collection was modified after the enumerator was instantiated.

## Standard Query Operators

Besides the methods on System.Object, any type that implements IEnumerable<T> is required to implement only one other method, GetEnumerator(). Yet, doing so makes more than 50 methods available to all types implementing IEnumerable<T>, not including any overloading—and this happens without needing to explicitly implement any method except the GetEnumerator() method. The additional functionality is provided through C# 3.0’s extension methods and resides in the class System.Linq.Enumerable. Therefore, including the using directive for System.Linq is all it takes to make these methods available.

Each method on IEnumerable<T> is a standard query operator; it provides querying capability over the collection on which it operates. In the following sections, we will examine some of the most prominent of these standard query operators. Many of these examples will depend on an Inventor and/or Patent class, both of which are defined in Listing 14.12.

### LISTING 14.12: Sample Classes for Use with Standard Query Operators

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

public class Patent
{
    // Title of the published application
    public string Title { get; set; }

    // The date the application was officially published
    public string YearOfPublication { get; set; }

    // A unique number assigned to published applications
    public string ApplicationNumber { get; set; }

    public long[] InventorIds { get; set; }

    public override string ToString()
    {
        return $"{ Title } ({ YearOfPublication })";
    }
}

public class Inventor
{
    public long Id { get; set; }
    public string Name { get; set; }
    public string City { get; set; }
    public string State { get; set; }
    public string Country { get; set; }

    public override string ToString()
    {
        return $"{ Name } ({ City }, { State })";
    }
}

class Program
{
    static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        Print(patents);

        Console.WriteLine();

        IEnumerable<Inventor> inventors = PatentData.Inventors;
        Print(inventors);
    }

    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}

public static class PatentData
{
    public static readonly Inventor[] Inventors = new Inventor[]
    {
        new Inventor(){
            Name="Benjamin Franklin", City="Philadelphia",
            State="PA", Country="USA", Id=1 },
```
