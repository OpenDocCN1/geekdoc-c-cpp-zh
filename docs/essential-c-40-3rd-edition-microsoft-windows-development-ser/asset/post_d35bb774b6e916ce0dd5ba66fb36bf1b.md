
Note that you cannot have a collection initializer for an anonymous type since the collection initializer requires a constructor call, and it is impossible to name the constructor. The workaround is to define a method such as `static List<T> CreateList<T>(T t) { return new List<T>(); }`. Method type inference allows the type parameter to be implied rather than specified explicitly, and so this workaround successfully allows for the creation of a collection of anonymous types.

Another approach to initializing a collection of anonymous types is to use an array initializer. Since it is not possible to specify the data type in the constructor, array initialization syntax allows for anonymous array initializers using new[] (see Listing 14.4).

### LISTING 14.4: Initializing Anonymous Type Arrays

```
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
                },
            },
            new
            {
                TeamName = "Italy",
                Players = new string[]
                {
                    "Gianluigi Buffon", "Angelo Peruzzi",
                    "Marco Amelia", "Cristian Zaccardo",
                    // ...
                },
            },
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

The resultant variable is an array of the anonymous type items, which must be homogenous since it is an array.

## What Makes a Class a Collection: IEnumerable<T>

By definition, a collection within .NET is a class that, at a minimum, implements IEnumerable<T> (technically, it would be the nongeneric type IEnumerable). This interface is a key because implementing the methods of IEnumerable<T> is the minimum implementation requirement needed to support iterating over the collection.

Chapter 3 showed how to use a foreach statement to iterate over an array of elements. The syntax is simple and avoids the complication of having to know how many elements there are. The runtime does not directly support the foreach statement, however. Instead, the C# compiler transforms the code as described in this section.

### foreach with Arrays

Listing 14.5 demonstrates a simple foreach loop iterating over an array of integers and then printing out each integer to the console.

### LISTING 14.5: foreach with Arrays

```
int[] array = new int[]{ 1, 2, 3, 4, 5, 6};
foreach (int item in array)
{
    Console.WriteLine(item);
}
```

From this code, the C# compiler creates a CIL equivalent of the for loop, as shown in Listing 14.6.

### LISTING 14.6: Compiled Implementation of foreach with Arrays

```
int number;
int[] tempArray;
int[] array = new int[]{1, 2, 3, 4, 5, 6};
tempArray = array;
for (int counter = 0; (counter < tempArray.Length); counter++)
{
    int item = tempArray[counter];
    Console.WriteLine(item);
}
```

In this example, note that foreach relies on support for the Length property and the index operator ([]). With the Length property, the C# compiler can use the for statement to iterate through each element in the array.

### foreach with IEnumerable<T>

Although the code shown in Listing 14.6 works well on arrays where the length is fixed and the index operator is always supported, not all types of collections have a known number of elements. Furthermore, many of the collection classes, including the Stack<T>, Queue<T>, and Dictionary<TKey, TValue> classes, do not support retrieving elements by index. Therefore, a more general approach of iterating over collections of elements is needed. The iterator pattern provides this capability. Assuming you can determine the first, next, and last elements, knowing the count and supporting retrieval of elements by index is unnecessary.

The System.Collections.Generic.IEnumerable<T> and nongeneric System.Collections.IEnumerable interfaces (see Listing 14.8) are designed to enable the iterator pattern for iterating over collections of elements, rather than the length-index pattern shown in Listing 14.6. A class diagram of their relationships appears in Figure 14.1.

![](img/ef1bd88b5fdf5fb56f8510479607fe66_596_0.png)

### FIGURE 14.1: IEnumerable<T> and IEnumerator Interfaces

IEnumerator, which IEnumerable<T> derives from, includes three members. The first is bool MoveNext(). Using this method, you can move from one element within the collection to the next while at the same time detecting when you have enumerated through every item. The second member, a read-only property called Current, returns the element currently in process. Current is overloaded in IEnumerable<T>, providing a type-specific implementation of it. With these two members on the collection class, it is possible to iterate over the collection simply using a while loop, as demonstrated in Listing 14.7. (The Reset() method usually throws a NotImplementedException and, therefore, should never be called. If you need to restart an enumeration, just create a fresh enumerator.)

### LISTING 14.7: Iterating over a Collection Using while

```
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

In Listing 14.7, the MoveNext() method returns false when it moves past the end of the collection. This replaces the need to count elements while looping.

Listing 14.7 uses a System.Collections.Generic.Stack<T> as the collection type. Numerous other collection types exist; this is just one example. The key trait of Stack<T> is its design as a last in, first out (LIFO) collection. It is important to note that the type parameter T identifies the type of all items within the collection. Collecting one particular type of object within a collection is a key characteristic of a generic collection. It is important that the programmer understands the data type within the collection when adding, removing, or accessing items within the collection.

This preceding example shows the gist of the C# compiler output, but it doesn't actually compile that way because it omits two important details concerning the implementation: interleaving and error handling.

### State Is Shared

The problem with an implementation such as Listing 14.7 is that if two such loops interleaved each other—one foreach inside another, both using the same collection—the collection must maintain a state indicator of the current element so that when MoveNext() is called, the next element can be determined. The problem is that one interleaving loop can affect the other. (The same is true of loops executed by multiple threads.)

To overcome this problem, the collection classes do not support IEnumerable<T> and IEnumerator interfaces directly. As shown in Figure 14.1, there is a second interface, called IEnumerable<T>, whose only method is GetEnumerator(). The purpose of this method is to return an object that supports IEnumerable<T>. Instead of the collection class maintaining the state, a different class, usually a nested class so that it has access to the internals of the collection, will support the IEnumerable<T> interface and will keep the state of the iteration loop. The enumerator is like a “cursor” or a “bookmark” in the sequence. You can have multiple bookmarks, and moving each of them enumerates over the collection independently of the other. Using this pattern, the C# equivalent of a foreach loop will look like the code shown in Listing 14.8.
