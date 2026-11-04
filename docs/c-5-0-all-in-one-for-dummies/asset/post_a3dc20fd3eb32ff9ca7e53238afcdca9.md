
```csharp
int index = Find(key);
if (index < 0)
{
    // It isn't -- find a new spot.
    index = FindEmpty();
    _keys[index] = key;
}

// Save the object in the corresponding spot.
_arrayElements[index] = value;

get
{
    int index = Find(key);
    if (index < 0)
    {
        return null;
    }
    return _arrayElements[index];
}
}
}

public class Program
{
    public static void Main(string[] args)
    {
        // Create an array with enough room.
        KeyedArray ma = new KeyedArray(100);

        // Save the ages of the Simpson kids.
        ma["Bart"] = 8;
        ma["Lisa"] = 10;
        ma["Maggie"] = 2;

        // Look up the age of Lisa.
        Console.WriteLine("Let's find Lisa's age");
        int age = (int)ma["Lisa"];
        Console.WriteLine("Lisa's age is {0}", age);

        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
}
```

The class KeyedArray holds two ordinary arrays. The _arrayElements array of objects contains the actual KeyedArray data. The strings that inhabit the _keys array act as identifiers for the object array. The ith element of _keys corresponds to the ith entry of _arrayElements. The application program can then index the KeyedArray via string identifiers that have meaning to the application.

![](img/80ff26f06fc9ab951e1cd4257b867366_170_0.png)

A noninteger index is referred to as a key. By the way, you can implement KeyedArray with an underlying List<T> instead of the fixed-size array. List<T> is indexable like an array because both implement the IList (or IList<T>) interface. This allows KeyedArray to be generic and to be much more flexible than using the inner array.

The set[string] indexer starts by checking to see whether the specified index already exists by calling the method Find(). If Find() returns an index, set[] stores the new data object into the corresponding index in _arrayElements. If Find() can't find the key, set[] calls FindEmpty() to return an empty slot in which to store the object provided.

The get[] side of the index follows similar logic. It first searches for the specified key using the Find() method. If Find() returns a nonnegative index, get[] returns the corresponding member of _arrayElements where the data is stored. If Find() returns -1, get[] returns null, indicating that it can't find the provided key anywhere in the list.

The Find() method loops through the members of _keys to look for the element with the same value as the string targetKey passed in. Find() returns the index of the found element (or -1 if none was found). FindEmpty() returns the index of the first element that has no key element.

Neither Find() nor FindEmpty() is written in an efficient manner. Any number of ways exist to make these methods faster, none of which has anything to do with indexers.

![](img/80ff26f06fc9ab951e1cd4257b867366_171_0.png)

Notice that you can't remove an element by providing a null key. As they used to say in college textbooks, "This problem is left as an exercise for the reader."

The Main() method demonstrates the Indexer class in a trivial way:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        // Create an array with enough room.
        KeyedArray ma = new KeyedArray(100);

        // Save the ages of the Simpson kids.
        ma["Bart"] = 8;
        ma["Lisa"] = 10;
        ma["Maggie"] = 2;

        // Look up the age of Lisa.
        Console.WriteLine("Let's find Lisa's age");
        int age = (int)ma["Lisa"];
        Console.WriteLine("Lisa is {0}", age);

        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

The program creates a KeyedArray object ma of length 100 (that is, with 100 free elements). It continues by storing the ages of the children in The Simpsons TV show, indexed by each child's name. Finally, the program retrieves Lisa's age using the expression ma [ "Lisa" ] and displays the result. The expression ma [ "Lisa" ] is read as "ma sub-Lisa."

Notice that the program has to cast the value returned from ma [ ] because KeyedArray is written to hold any type of object. The cast wouldn't be necessary if the indexer were written to handle only int values — or if the KeyedArray were generic. (For more information about generics, see Chapter 8 in this minibook.)

The output of the program is simple yet elegant:

```
Let's find Lisa's age
Lisa is 10
Press Enter to terminate...
```

As an aside, the IList interface describes a class that provides an array-like integer indexer of the form object this[int]. C# also has an IList<T> interface, which you can use to replace object with your choice of type T. This would eliminate the need for a cast in the previous example.

For a generic version of the Indexer program, see the IndexerGeneric example on this book's website.

![](img/80ff26f06fc9ab951e1cd4257b867366_172_0.png)

## Looping Around the Iterator Block

In previous versions of C#, the linked list we discuss in the section "Accessing Collections the Array Way: Indexes," earlier in this chapter, was the primary practice for moving through collections, just like it was done in C++ and C before this. While that solution does work, it turns out that C# 2.0 has simplified this process so that

- You don't have to call GetEnumerator() (and cast the results).
- You don't have to call MoveNext().
- You don't have to call Current and cast its return value.
- You can simply use foreach to iterate the collection. (C# does the rest for you under the hood — it even writes the enumerator class.)

Well, to be fair, foreach works for the LinkedList class in .NET, too. That comes from providing a GetEnumerator() method. But I still had to write the LinkedListIterator class myself. The new wrinkle is that you can skip that part in your roll-your-own collection classes, if you choose.

Rather than implement all those interface methods in collection classes you write, you can provide an iterator block — and you don’t have to write your own iterator class to support the collection. You can use iterator blocks for a host of other chores, too, as I show you in the next example.

The best approach to iteration now uses iterator blocks. When you write a collection class — and the need still exists for custom collection classes such as `KeyedList` and `PriorityQueue` — you implement an iterator block in its code rather than implement the `IEnumerator` interface. Then users of that class can simply iterate the collection with `foreach`. I walk you through it a piece at a time, to show you several variations on iterator blocks.

Every example in this section is part of the `IteratorBlocks` example on this book’s website:

![](img/80ff26f06fc9ab951e1cd4257b867366_173_0.png)

```csharp
// IteratorBlocks -- Demonstrates using the C# 2.0 iterator
//     block approach to writing collection iterators
using System;
namespace IteratorBlocks
{
    class IteratorBlocks
    {
        //Main -- Demonstrate five different applications of
        // iterator blocks.
        static void Main(string[] args)
        {
            // Instantiate a MonthDays "collection" class.
            MonthDays md = new MonthDays();
            // Iterate it.
            Console.WriteLine("Stream of months:\n");
            foreach (string month in md)
            {
                Console.WriteLine(month);
            }

            // Instantiate a StringChunks "collection" class.
            StringChunks sc = new StringChunks();
            // Iterate it: prints pieces of text.
            // This iteration puts each chunk on its own line.
            Console.WriteLine("\nStream of string chunks:\n");
            foreach (string chunk in sc)
            {
                Console.WriteLine(chunk);
            }

            // And this iteration puts it all on one line.
            Console.WriteLine("\nStream of string chunks on one line:\n");
            foreach (string chunk in sc)
            {
                Console.Write(chunk);
            }
            Console.WriteLine();

            // Instantiate a YieldBreakEx "collection" class.
            YieldBreakEx yb = new YieldBreakEx();
            // Iterate it, but stop after 13.
            Console.WriteLine("\nStream of primes:\n");
```
