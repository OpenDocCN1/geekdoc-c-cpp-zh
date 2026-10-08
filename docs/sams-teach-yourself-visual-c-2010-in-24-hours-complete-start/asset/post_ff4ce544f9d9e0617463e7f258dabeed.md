
By enabling object initializers inside a collection initializer, it becomes possible to use collection initializers for any type of collection, including dictionaries, whose Add method takes multiple parameters.

## Collection Interfaces

If you look back over the common members and properties for all the different collections, you should notice some similarities and consistency in their public interfaces. This consistency stems from a set of interfaces that these collection classes implement. Some classes implement more interfaces than others do, but all of them implement at least one interface.

The collection interfaces can be divided into those that provide specific collection implementation contracts and those that provide supporting implementations, such as comparison and enumeration features. In the first group, those that provide specific collection behavior, there are just four interfaces:

- **ICollection<>** defines the methods and properties for manipulating generic collections.
- **IList<T>** extends **ICollection<>** to provide the methods and properties for manipulating generic collections whose elements can be individually accessed by index.
- **IDictionary<TKey, TValue>** extends **ICollection<>** to provide the methods and properties for manipulating generic collections of key/value pairs in which each pair must have a unique key.
- **ISet<T>** extends **ICollection<>** to provide the methods and properties for manipulating generic collections that have unique elements and provide set operations.

The second group also contains only four interfaces, as follows:

- **IComparer<T>** defines a method to compare two objects. This interface is used with the **List<\>**.Sort and **List<\>**.BinarySearch methods and provides a way to customize the sort order of a collection. The **Comparer<\>** class provides a default implementation of this interface and is usually sufficient for most requirements.
- **IEnumerable<>** extends **IEnumerable** and provides support for simple iteration over a collection by exposing an enumerator. This interface is included for parity with the non-generic collections, and by implementing this interface, a generic collection can be used any time an **IEnumerable** is expected.
- **IEnumerable<T>** also provides support for simple iteration over a collection.
- **IEqualityComparer<T>** provides a way for you to provide your own definition of equality for type T. The **EqualityComparer<T>** class provides a default implementation of this interface and is usually sufficient for most requirements.

## Enumerable Objects and Iterators

If you look at the definitions given for IEnumerable<T> and IEnumerator<T>, you notice that they are similar. These interfaces (and their non-generic counterparts) comprise what is commonly referred to as the *iterator pattern*.

This pattern essentially enables you to ask an object that implements IEnumerable<T>, otherwise known as an **enumerable object**, for an enumerator (an object that implements IEnumerator<T>). When you have an IEnumerator<T>, you can then enumerate (or iterate) over the data one element at a time.

For example, the code in Listing 9.5 shows a typical foreach statement that iterates over the contents of an integer list, printing each value.

### LISTING 9.5 A Simple foreach Statement

```csharp
List<int> list = new List<int>() { 0, 2, 4, 6, 8 };
foreach(int i in list)
{
    Console.WriteLine(i);
}
```

This code is actually translated by the compiler into something that looks approximately like the code shown in Listing 9.6.

### LISTING 9.6 The Compiler Expanded foreach Statement

```csharp
List<int> list = new List<int>() { 0, 2, 4, 6, 8 };
IEnumerator<int> iterator = ((IEnumerable<int>)list).GetEnumerator();
while (iterator.MoveNext())
{
    Console.WriteLine(iterator.Current);
}
```

The GetEnumerator method is defined by the IEnumerable<T> interface (in fact, it's the only member defined by the interface) and simply provides a way for the enumerable object to expose an enumerator. It is the enumerator, through the MoveNext method and Current property (defined by the IEnumerator<T> and IEnumerator interfaces), that enables you to move forward through the data contained in the enumerable object.

## Why Two Interfaces?

By keeping a distinction between an enumerable object (**IEnumerable<T>**) and an enumerator over that object (**IEnumerator<T>**), you can perform multiple iterations over the same enumerable source. Obviously, you don’t want the iterations interfering with each other as they move through the data, so you need two independent representations (enumerators) providing you the current data element and the mechanism to move to the next one.

## By the Way

Fortunately, all the generic collections (and the non-generic ones as well) implement **IEnumerable<T>**, **IEnumerable**, **IEnumerator<T>**, and **IEnumerator** already, so you can use them without the extra complexity of writing the iterator mechanism yourself.

What happens if you want your own class to offer similar behavior? You can certainly make your class implement **IEnumerable<T>** and then write your own **IEnumerator<T>** derived class, but doing so isn’t necessary if you use an iterator. This enables the compiler to do all the hard work for you.

An iterator is a method, property get accessor, or operator that returns an ordered sequence of values all of which are the same type. The `yield` keyword tells the compiler the block it appears in is an iterator block. A `yield` return statement returns each element, and a `yield` break statement ends the iteration. The body of such an iterator method, accessor, or operator has the following restrictions:

- Unsafe blocks are not permitted.
- Parameters cannot be ref or out parameters.
- A `yield` return statement cannot be located anywhere within a try-catch block. It can be located in a try block if it is followed by a `finally` block.
- A `yield` break statement can be located in either a try block or a catch block, but not in a `finally` block.
- A `yield` statement cannot be in an anonymous method.

Listing 9.7 shows code that would produce the same output as that shown in Listing 9.6 using an iterator instead.

## LISTING 9.7 A Simple Iterator

```csharp
class Program
{
    static IEnumerable<int> GetEvenNumbers()
    {
        yield return 0;
        yield return 2;
        yield return 4;
        yield return 6;
        yield return 8;
    }

    static void Main()
    {
        foreach(int i in GetEvenNumbers())
        {
            Console.WriteLine(i);
        }
    }
}
```

Iterators can do much more than simply yield values. As long as you abide by the restrictions previously mentioned, iterators can have any degree of sophistication in how they determine the values to yield. Listing 9.8 produces the same output as that from Listing 9.7 but does so using a more complex iterator.

## LISTING 9.8 A More Complex Iterator

```csharp
class Program
{
    static IEnumerable<int> GetEvenNumbers()
    {
        for (int i = 0; i <= 9; i++)
        {
            if (i % 2 == 0)
            {
                yield return i;
            }
        }
    }

    static void Main()
    {
        foreach(int i in GetEvenNumbers())
        {
            Console.WriteLine(i);
        }
    }
}
```

## Summary

In this hour, you have learned how to work with large amounts of data using arrays and collections. Arrays are the simplest type of collection and have direct language support, whereas the other collection types, such as List<T> and Stack<T>, offer more flexibility and enable you to create your own specialized collections. You also learned how indexers enable your own classes to provide the same type of index-based access that arrays and collections offer. Finally, you looked at the different collection interfaces available and saw how you can easily declare and initialize both arrays and collections using initializer syntax.

This completes your programming foundation. You now know the language syntax and fundamentals of creating your own classes, structs, enums, and collections, and how to manipulate string data and control program flow.

## Q&A

- **Q.** What is an array?
  **A.** An array is a numerically indexed collection of objects that are all of the same compile-time type.

- **Q.** Are arrays in C# zero-based or one-based?
  **A.** Arrays in C# use a zero-based indexing scheme.

- **Q.** Can arrays in C# be resized?
  **A.** Arrays in C# can be indirectly resized using the `Array.Resize` static method, which creates a new array, if needed, and copying the values from the old array to the new one.

- **Q.** What is an indexer?
  **A.** An indexer is a special type of property that enables a class to be indexed like an array. Indexers are identified by signature rather than by name and must be an instance member.

- **Q.** What is the `List<>` collection?
  **A.** The `List<>` collection is the most commonly used collection and is similar to an array but is dynamically sized as needed.

- **Q.** What is a dictionary?
  **A.** A dictionary is a collection that does not enable duplicates that can provide a mapping between a set of keys and a set of values.
