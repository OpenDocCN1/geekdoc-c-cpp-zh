
# What Makes a Class a Collection: IEnumerable

LISTING 15.6: A Separate Enumerator Maintaining State during an Iteration

```
System.Collections.Generic.Stack<int> stack =
new();
int number;
System.Collections.Generic.Stack<int>.Enumerator
enumerator;
// ...
// If IEnumerable<T> is implemented explicitly,
// then a cast is ((IEnumerable<int>)stack).GetEnumerator();
enumerator = stack.GetEnumerator();
while (enumerator.MoveNext())
{
    number = enumerator.Current;
    Console.WriteLine(number);
}
```

# ADVANCED/BEGINNER TOPIC

# Cleaning Up Following Iteration

Given that the classes that implement the IEnumerator<T> interface maintain the state, sometimes you need to clean up the state after it exits the loop (because either all iterations have completed or an exception is thrown). To achieve this, the IEnumerator<T> interface derives from IDisposable. Enumerators that implement IEnumerator do not necessarily implement IDisposable, but if they do, Dispose() will be called as well. This means that Dispose() can be called after the foreach loop. The C# equivalent of the final Common Intermediate Language (CIL) code, therefore, looks like Listing 15.7.

LISTING 15.7: Compiled Result of foreach on Collections

```
System.Collections.Generic.Stack<int> stack = new();
System.Collections.Generic.Stack<int>.Enumerator enumerator;
IDisposable disposable;
```

```
enumerator = stack.GetEnumerator();
try
{}
```

# Chapter 15: Collection Interfaces with Standard Query Operators

```c
int number;
while (enumerator.MoveNext())
{
    number = enumerator.Current;
    Console.WriteLine(number);
}
```

// Explicit cast used for IEnumerator<T>
disposable = (IDisposable)enumerator;
disposable.Dispose();

// IEnumerator will use the as operator unless IDisposable
// support is known at compile time
var disposable = (enumerator as IDisposable);
// if (disposable != null)
// {
//     disposable.Dispose();
// }
```

Notice that because the IDisposable interface is supported by IEnumerator<T>, the using statement can simplify the code in Listing 15.7 to that shown in Listing 15.8.

LISTING 15.8: Error Handling and Resource Cleanup using System.Collections.Generic.Stack<int> stack = new(); int number;

```csharp
using
System.Collections.Generic.Stack<int>.Enumerator
enumerator = stack.GetEnumerator()
while (enumerator.MoveNext())
{
    number = enumerator.Current;
    Console.WriteLine(number);
}
```

# What Makes a Class a Collection: IEnumerable

However, recall that the CIL does not directly support the using keyword. For this reason, the code in Listing 15.7 is actually a more accurate C# representation of the foreach CIL code.

# ADVANCED TOPIC

foreach without IEnumerable
C# doesn't require that IEnumerable/IEnumerable<T> be implemented to iterate over a data type using foreach. Rather, the compiler uses a concept known as duck typing: It looks for a GetEnumerator() method that returns a type with a Current property and a Next(). Duck typing searches by name rather than relying on an interface or explicit method to the method. (The name “duck typing” comes from the idea that to be treated as a duck, the object must implement a Quack() method; it need not implement an IInterface.) If duck typing fails to find a suitable implementation of the enumerable pattern, the compiler checks whether the collection implements the interfaces. Furthermore, even if neither the nor the interface exist, starting in C# 9.0, the compiler will look for an extension method that implements the GetEnumerator() signature, and will use that if it is available.

# Do Not Modify Collections during foreach Iteration

Chapter 4 showed that the compiler prevents assignment of the foreach variable (number). As demonstrated in Listing 15.7, an assignment to number would not change the collection element itself, so the C# compiler prevents such an assignment altogether.

In addition, neither the element count within a collection nor the items themselves can generally be modified during the execution of a foreach loop. If, for example, you called stack.Push(42) inside the foreach loop, it would be ambiguous whether the iterator should ignore or incorporate the change to stack—in other words, iterator should iterate over the newly added item or ignore and assume the same state as when it was instantiated.

Because of this ambiguity, an exception of type System.InvalidOperationException is generally thrown upon accessing the enumerator within a foreach loop. This exception reports that the collection was modified after the enumerator was instantiated.

# Standard Query Operators

Besides the methods on System.Object, any type that implements IEnumerable<T> is required to implement only one other method, GetEnumerator(). By doing so makes more than 50 methods available to all types implementing IEnumerable<T>, not including any overloading—and this happens without needing to explicitly implement any method except the GetEnumerator() method. The additional functionality is provided through extension methods and resides in the class System.Linq.Enumerable. Therefore, including the using declarative for System.Linq is all it takes to make these methods available.

Each method on IEnumerable<T> is a standard query operator; it provides querying capability over the collection on which it operates. In the following sections, we examine some of the most prominent of these standard query operators. Many of these examples depend on an Inventor and/or Patent class, both of which are defined in Listing 15.9 with Output 15.1.

LISTING 15.9: Sample Classes for Use with Standard Query Operators

```csharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        Print(patents);
    }

    Console.WriteLine();
}
```

8. Starting in C# 3.0.

```csharp
IEnumerable<Inventor> inventors = PatentData.Inventors;
Print(inventors);

private static void Print<T>(IEnumerable<T> items)
{
  foreach(T item in items)
  {
    Console.WriteLine(item);
  }
}
```

# OUTPUT 15.1

- Bifocals (1784)
- Phonograph (1877)
- Kinetoscope (1888)
- Electrical Telegraph (1837)
- Flying Machine (1903)
- Steam Locomotive (1815)
- Droplet Deposition Apparatus (1989)
- Backless Brassiere (1914)

- Bifocals (1784)
- Phonograph (1877)
- Kinetoscope (1888)
- Electrical Telegraph (1837)
- Flying Machine (1903)
- Steam Locomotive (1815)
- Droplet Deposition Apparatus (1989)
- Backless Brassiere (1914)

# Filtering with Where()

To filter data from a collection, we need to provide a filter method that returns true or false, indicating whether or not a element is included. A delegate expression that takes an argument and returns a Boolean value is called a **predicate**, and a collection's Where() method depends on predicates, as shown in 15.10. (Technically, the result of the Where() is an **object** that encapsulates the operation of filtering a sequence with a predicate). The results appear in 15.2.

# Chapter 15: Collection Interfaces with Standard Query Operators

LISTING 15.10: Filtering with System.Linq.Where()

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
```

```csharp
public class Program
{
    public static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        patents = patents.Where(patent -> patent.YearOfPublication.StartsWith("18"));
        Print(patents);
    }
}
```

# OUTPUT 15.2

| Phonograph (1877) |
| Kinetoscope (1888) |
| Electrical Telegraph (1837) |
| Steam Locomotive (1815) |
