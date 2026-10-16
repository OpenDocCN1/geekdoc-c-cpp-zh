
## 11 Collections

- Understanding collection interfaces and types
- Working with lists, queues, and stacks
- Working with linked and sorted lists
- Using dictionaries and sets
- Evaluating performance

The wrox.com code downloads for this chapter are found at http://www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- List Samples
- Queue Sample
- Linked List Sample
- Sorted List Sample
- Dictionary Sample
- Set Sample

Chapter 7, “Arrays and Tuples,” covers arrays and the interfaces implemented by the Array class. The size of arrays is fixed. If the number of elements is dynamic, you should use a collection class instead of an array.

List<T> is a collection class that can be compared to arrays; but there are also other kinds of collections: queues, stacks, linked lists, dictionaries, and sets. The other collection classes have partly different APIs to access the elements in the collection and often a different internal structure for how the items are stored in memory. This chapter covers all of these collection classes and their differences, including performance differences.

This chapter also discusses bit arrays and concurrent collections that can be used from multiple threads.

Most collection classes are in the `System.Collections` and `System.Collections.Generic` namespaces. Generic collection classes are located in the `System.Collections.Generic` namespace. Collection classes that are specialized for a specific type are located in the `System.Collections.Specialized` namespace. Thread-safe collection classes are in the `System.Collections.Concurrent` namespace. Immutable collection classes are in the `System.Collections.Immutable` namespace.

Of course, there are also other ways to group collection classes. Collections can be grouped into lists, collections, and dictionaries based on the interfaces that are implemented by the collection class.

> **NOTE** *You can read detailed information about the interfaces `IEnumerable` and `IEnumerator` in Chapter 7.*

The following table describes the most important interfaces implemented by collections and lists.

| Interface | Description |
|---|---|
| `IEnumerable<T>` | The interface `IEnumerable` is required by the `foreach` statement. This interface defines the method `GetEnumerator`, which returns an enumerator that implements the `IEnumerator` interface. |
| `ICollection<T>` | `ICollection<T>` is implemented by generic collection classes. With this you can get the number of items in the collection (`Count` property), and copy the collection to an array (`CopyTo` method). You can also add and remove items from the collection (`Add`, `Remove`, `Clear`). |
| `IList<T>` | The `IList<T>` interface is for lists where elements can be accessed from their position. This interface defines an indexer, as well as ways to insert or remove items from specific positions (`Insert`, `RemoveAt` methods). `IList<T>` derives from `ICollection<T>`. |
| `ISet<T>` | This interface is implemented by sets. Sets allow combining different sets into a union, getting the intersection of two sets, and checking whether two sets overlap. `ISet<T>` derives from `ICollection<T>`. |
| `IDictionary<TKey, TValue>` | The interface `IDictionary<TKey, TValue>` is implemented by generic collection classes that have a key and a value. With this interface all the keys and values can be accessed, items can be accessed with an indexer of type `key`, and items can be added or removed. |
| `ILookup<TKey, TValue>` | Similar to the `IDictionary<TKey, TValue>` interface, lookups have keys and values. However, with lookups the collection can contain multiple values with one key. |
| `IComparer<T>` | The interface `IComparer<T>` is implemented by a comparer and used to sort elements inside a collection with the `Compare` method. |
| `IEqualityComparer<T>` | `IEqualityComparer<T>` is implemented by a comparer that can be used for keys in a dictionary. With this interface the objects can be compared for equality. |

### Lists

For resizable lists, the .NET Framework offers the generic class `List<T>`. This class implements the `IList`, `ICollection`, `IEnumerable`, `IList<T>`, `ICollection<T>`, and `IEnumerable<T>` interfaces.

The following examples use the members of the class Racer as elements to be added to the collection to represent a Formula-1 racer. This class has five properties: Id, FirstName, LastName, Country, and the number of Wins. With the constructors of the class, the name of the racer and the number of wins can be passed to set the members. The method ToString is overridden to return the name of the racer. The class Racer also implements the generic interface `IComparable<T>` for sorting racer elements and `IFormattable` (code file ListSamples/Racer.cs):

```
public class Racer: IComparable<Racer>, IFormattable
{
    public int Id { get; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Country { get; set; }
    public int Wins { get; set; }

    public Racer(int id, string firstName, string lastName, string country)
        : this(id, firstName, lastName, country, wins: 0)
    { }

    public Racer(int id, string firstName, string lastName, string country, int wins)
    {
        Id = id;
        FirstName = firstName;
        LastName = lastName;
        Country = country;
        Wins = wins;
    }
    public override string ToString() => $"{FirstName} {LastName}";
    public string ToString(string format, IFormatProvider formatProvider)
    {
        if (format == null) format = "N";
        switch (format.ToUpper())
        {
            case "N": // name
                return ToString();
            case "F": // first name
                return FirstName;
            case "L": // last name
                return LastName;
            case "W": // Wins
                return $"{ToString()}, Wins: {Wins}";
            case "C": // Country
                return $"{ToString()}, Country: {Country}";
            case "A": // All
                return $"{ToString()}, Country: {Country} Wins: {Wins}";
            default:
                throw new FormatException(String.Format(formatProvider, $"Format {format} is not supported"));
        }
    }
    public string ToString(string format) => ToString(format, null);
    public int CompareTo(Racer other)
    {
        int compare = LastName?.CompareTo(other?.LastName) ?? -1;
        if (compare == 0)
        {
            return FirstName?.CompareTo(other?.FirstName) ?? -1;
        }
        return compare;
    }
}
```

### Creating Lists

You can create list objects by invoking the default constructor. With the generic class `List<T>`, you must specify the type for the values of the list with the declaration. The following code shows how to declare a `List<T>` with `int` and a list with `Racer` elements. `ArrayList` is a non-generic list that accepts any `Object` type for its elements.

Using the default constructor creates an empty list. As soon as elements are added to the list, the capacity of the list is extended to allow 4 elements. If the fifth element is added, the list is resized to allow 8 elements. If 8 elements are not enough, the list is resized again to contain 16 elements. With every resize the capacity of the list is doubled.

```
var intList = new List<int>();
var racers = new List<Racer>();
```

When the capacity of the list changes, the complete collection is reallocated to a new memory block. With the implementation of `List<T>`, an array of type `T` is used. With reallocation, a new array is created, and `Array.Copy` copies the elements from the old array to the new array. To save time, if you know in advance the number of elements that should be in the list, you can define the capacity with the constructor. The following example creates a collection with a capacity of 10 elements. If the capacity is not large enough for the elements added, the capacity is resized to 20 and then to 40 elements—doubled again:

```
List<int> intList = new List<int>(10);
```

You can get and set the capacity of a collection by using the `Capacity` property:

```
intList.Capacity = 20;
```

The capacity is not the same as the number of elements in the collection. The number of elements in the collection can be read with the `Count` property. Of course, the capacity is always larger or equal to the number of items. As long as no element was added to the list, the count is 0:

```
WriteLine(intList.Count);
```
