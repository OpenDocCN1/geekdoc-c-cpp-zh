
take parameters that are compatible with the values specified in the collection initializer.

For dictionaries, the collection initializer syntax is slightly more complex, because each element in the dictionary requires both the key and the value. This syntax is shown in Listing 14.4.

**Listing 14.4: Initializing Dictionaries**

```csharp
using System;
using System.Collections.Generic;
#if !PRECSHARP6
    // C# 6.0 or Later
    Dictionary<string, ConsoleColor> colorMap =
        new Dictionary<string, ConsoleColor>
        {
            ["Error"] = ConsoleColor.Red,
            ["Warning"] = ConsoleColor.Yellow,
            ["Information"] = ConsoleColor.Green,
            ["Verbose"] = ConsoleColor.White
        };
#else
    // Before C# 6.0
    Dictionary<string, ConsoleColor> colorMap =
        new Dictionary<string, ConsoleColor>
        {
            { "Error", ConsoleColor.Red },
            { "Warning", ConsoleColor.Yellow },
            { "Information", ConsoleColor.Green },
            { "Verbose", ConsoleColor.White}
        };
#endif
```

This listing actually includes two different versions of the initialization. The first demonstrates a new syntax introduced in C# 6.0, which expresses the intent of a name/value pair by allowing the assignment operator to express which value is associated with which key. The second syntax (which still works with C# 6.0 or later) pairs the name and the value together using curly brackets.

Allowing initializers on collections that don’t support `ICollection<T>` was important for two reasons. First, the majority of collections (types that implement `IEnumerable<T>`) do not also implement `ICollection<T>`, which significantly reduces the usefulness of collection initializers. Second, matching on the method name and signature compatibility with the collection initializer items enables greater diversity in the items initialized into the collection. For example, the initializer now can support `new DataStore(){ a, {b, c}}` as long as there is one `Add()` method whose signature is compatible with parameter `a`, and a second `Add()` method whose signature is compatible with `b`, `c`.

Note that you cannot have a collection initializer for an anonymous type since the collection initializer requires a constructor call, and it is impossible to name the constructor. The workaround is to define a method such as `static List<T> CreateList<T>(T t) { return new List<T>(); }`. Method type inference allows the type parameter to be implied rather than specified explicitly, so this workaround successfully allows for the creation of a collection of anonymous types.

Another approach to initializing a collection of anonymous types is to use an array initializer. As it is not possible to specify the data type in the constructor, array initialization syntax allows for anonymous array initializers using `new[]` (see Listing 14.5).

**Listing 14.5: Initializing Anonymous Type Arrays**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        var worldCup2006Finalists = new[]
        {
            new
            {
                TeamName = "France",
                Players = new string[]
                {
                    "Fabien Barthez", "Gregory Coupet",
                    "Mickael Landreau", "Eric Abidal",
                    // ...
                }
            },
            new
            {
                TeamName = "Italy",
                Players = new string[]
                {
                    "Gianluigi Buffon", "Angelo Peruzzi",
                    "Marco Amelia", "Cristian Zaccardo",
                    // ...
                }
            }
        };

        Print(worldCup2006Finalists);
    }

    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}
```

The resultant variable is an array of the anonymous type items, which must be homogeneous because it is an array.

## What Makes a Class a Collection: IEnumerable<T>

By definition, a collection within .NET is a class that, at a minimum, implements `IEnumerable<T>` (or the nongeneric type `IEnumerable`). This interface is critical because implementing the methods of `IEnumerable<T>` is the minimum needed to support iterating over the collection.

Chapter 3 showed how to use a foreach statement to iterate over an array of elements. This syntax is simple and avoids the complication of having to know how many elements there are. The runtime does not directly support the foreach statement, however. Instead, the C# compiler transforms the code as described in this section.

### foreach with Arrays

Listing 14.6 demonstrates a simple foreach loop iterating over an array of integers and then printing out each integer to the console.

**Listing 14.6: foreach with Arrays**

```csharp
int[] array = new int[]{1, 2, 3, 4, 5, 6};

foreach (int item in array)
{
    Console.WriteLine(item);
}
```

From this code, the C# compiler creates a CIL equivalent of the for loop, as shown in Listing 14.7.

**Listing 14.7: Compiled Implementation of foreach with Arrays**

```csharp
int[] tempArray;
int[] array = new int[]{1, 2, 3, 4, 5, 6};

tempArray = array;
for (int counter = 0; (counter < tempArray.Length); counter++)
{
    int item = tempArray[counter];

    Console.WriteLine(item);
}
```

In this example, note that foreach relies on support for the `Length` property and the index operator (`[]`). With the `Length` property, the C# compiler can use the `for` statement to iterate through each element in the array.

### foreach with IEnumerable<T>

Although the code shown in Listing 14.7 works well on arrays where the length is fixed and the index operator is always supported, not all types of collections have a known number of elements. Furthermore, many of the collection classes, including the `Stack<T>`, `Queue<T>`, and `Dictionary<TKey, TValue>` classes, do not support retrieving elements by index. Therefore, a more general approach of iterating over collections of elements is needed. The iterator pattern provides this capability. Assuming you can determine the first, next, and last elements, knowing the count and supporting retrieval of elements by index is unnecessary.

The `System.Collections.Generic.IEnumerator<T>` and nongeneric `System.Collections.IEnumerator` interfaces (see Listing 14.9) are designed to enable the iterator pattern for iterating over collections of elements, rather than the length–index pattern shown in Listing 14.7. A class diagram of their relationships appears in Figure 14.1.

![](img/25683ccec0773ba5b8794b11f2b12877_622_0.png)

**Figure 14.1:** A Class Diagram of `IEnumerator<T>` and `IEnumerator` Interfaces

`IEnumerator`, which `IEnumerator<T>` derives from, includes three members. The first is `bool MoveNext()`. Using this method, you can move from one element within the collection to the next, while at the same time detecting when you have enumerated through every item. The second member, a read-only property called `Current`, returns the element currently in process. `Current` is overloaded in `IEnumerator<T>`, providing a type-specific implementation of it. With these two members on the collection class, it is possible to iterate over the collection simply using a while loop, as demonstrated in Listing 14.8. (The `Reset()` method usually throws a `NotImplemented` Exception, so it should never be called. If you need to restart an enumeration, just create a fresh enumerator.)

**Listing 14.8: Iterating over a Collection Using while**

```csharp
System.Collections.Generic.Stack<int> stack =
    new System.Collections.Generic.Stack<int>();
int number;
// ...

// This code is conceptual, not the actual code.
while (stack.MoveNext())
{
    number = stack.Current;
    Console.WriteLine(number);
}
```

In Listing 14.8, the `MoveNext()` method returns false when it moves past the end of the collection. This replaces the need to count elements while looping.

Listing 14.8 uses a `System.Collections.Generic.Stack<T>` as the collection type. Numerous other collection types exist; this is just one example. The key trait of `Stack<T>` is its design as a “last in, first out” (LIFO) collection. Notice that the type parameter `T` identifies the type of all items within the collection. Collecting one particular type of object within a collection is a key characteristic of a generic collection. The programmer must know the data type within the collection when adding, removing, or accessing items within the collection.
