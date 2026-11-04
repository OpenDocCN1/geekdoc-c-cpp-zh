
Figure 19.1 lists some of the collection interfaces in namespace `System.Collections.Generic`, which also have legacy object-based analogs in `System.Collections`. Many collection classes implement these interfaces. You may also provide implementations specific to your own requirements.

| Interface | Description |
|---|---|
| `IEnumerable<T>` | An object that can be enumerated—for example, a `foreach` loop can iterate over such an object’s elements. This interface contains one method, `GetEnumerator`, which returns an `IEnumerator<T>` object, which (as you’ll see in Section 19.3) can be used to iterate through a collection. In fact, `foreach` uses a collection’s `IEnumerator<T>` object behind the scenes. `ICollection<T>` extends `IEnumerable<T>` so all collection classes implement `IEnumerable<T>` directly or indirectly. |
| `ICollection<T>` | The interface from which interfaces `IList<T>` and `IDictionary<K,V>` inherit. Contains a `Count` property to determine the size of a collection and a `CopyTo` method for copying a collection’s contents to a traditional array, and an `IsReadOnly` property. |
| `IList<T>` | An ordered collection that can be manipulated like an array. Provides a `[]` operator (known as an indexer) for accessing elements with an int index. Also has methods for searching and modifying a collection, including `Add`, `Remove`, `Contains` and `IndexOf`. |
| `IDictionary<K,V>` | A collection of values, indexed by an arbitrary “key” object of type K. Provides an indexer (`[]`) for accessing elements by key and methods for modifying the collection (e.g., `Add`, `Remove`). `IDictionary<K,V>` property `Keys` contains all the keys, and property `Values` contains all the stored values. |

**Fig. 19.1**  |  Some common generic collection interfaces.

## Namespace `System.Collections.Generic`

With the collections of the `System.Collections.Generic` namespace, you can specify the exact type that will be stored in a collection. This provides two key benefits over the object-based legacy collections:

- *Compile-time type checking* ensures that you’re using appropriate types with your collection and, if not, the compiler issues error messages.
- Any item you retrieve from a generic collection will have the correct type. With object-based collections, any item you retrieve is returned as an object. Then, you must *explicitly cast* the object to the type that your program manipulates. This could lead to `InvalidCastException`s at execution time if the referenced object does not have the appropriate type.

Generic collections are especially useful for storing value types, since they eliminate the overhead of boxing and unboxing required with object-based legacy collections.

In this chapter, we continue our discussion of data structures and collections with additional built-in array capabilities, as well as the generic SortedDictionary and LinkedList classes. Namespace System.Collections.Generic provides many other data structures, including Stack<T>, Queue<T> and SortedList<K,V> (a collection of key–value pairs that are sorted by key and can be accessed either by key or by index). Figure 19.2 summarizes many of the collection classes—for a complete list, visit

```
https://msdn.microsoft.com/library/system.collections.generic
```

The collection classes have many common capabilities specified by the interfaces the classes implement. Once you know how to use a few collections (like List, Dictionary, LinkedList and SortedDictionary), you can figure out how to use the others via their online documentation, which includes sample code.

| Class | Implements interface | Description |
|---|---|---|
| *System namespace* |  |  |
| Array | IList | The base class of all conventional arrays. See Section 19.3. |
| *System.Collections.Generic namespace* |  |  |
| Dictionary<K, V> | IDictionary<K, V> | A generic, unordered collection of key–value pairs that can be accessed rapidly by key. See Section 17.9.2. |
| LinkedList<T> | ICollection<T> | A generic doubly linked list. See Section 19.5. |
| List<T> | IList<T> | A generic array-based list. See Section 9.4. |
| Queue<T> | ICollection<T> | A generic first-in, first-out (FIFO) collection. |
| SortedDictionary<K, V> | IDictionary<K, V> | A dictionary that sorts the data by the keys in a binary tree. See Section 19.4. |
| SortedList<K, V> | IDictionary<K, V> | Similar to a SortedDictionary, but uses arrays internally. If the data already exists and is sorted before insertion in a collection, then inserting in a SortedList is faster than a SortedDictionary. If the data is not sorted, insertion in a SortedDictionary is faster. |
| Stack<T> | ICollection<T> | A generic last-in, first-out (LIFO) collection. |
| *Legacy collections of the System.Collections namespace* |  |  |
| ArrayList | IList | Mimics conventional arrays, but will grow or shrink as needed to accommodate the number of elements. |

**Fig. 19.2** | Some .NET Framework collection classes. (Part 1 of 2.)

| Class | Implements interface | Description |
|---|---|---|
| BitArray | ICollection | A memory-efficient array of bits in which each bit's 0 or 1 value represents the bool value false or true. |
| Hashtable | IDictionary | An unordered collection of key-value pairs that can be accessed rapidly by key. |
| Queue | ICollection | A first-in, first-out (FIFO) collection. |
| SortedList | IDictionary | A collection of key-value pairs that are sorted by key and can be accessed either by key or by index. |
| Stack | ICollection | A last-in, first-out (LIFO) collection. |

**Fig. 19.2** | Some .NET Framework collection classes. (Part 2 of 2.)

We also discuss the `IEnumerator<T>` interface. Each collection class's enumerator allows you to iterate through the collection. Although these enumerators have different implementations, they all implement the `IEnumerator<T>` interface so that an app can iterate through a collection's elements (e.g., with a foreach statement). In the next section, we begin our discussion by examining enumerators and the capabilities for array manipulation. Collection classes directly or indirectly implement `ICollection<T>` and `IEnumerable<T>` (or their object-based equivalents `ICollection` and `IEnumerable` for legacy collections).

### 19.3 Class Array and Enumerators

Chapter 8 presented basic array-processing capabilities. All arrays implicitly inherit from abstract base class Array (namespace `System`); this class defines property `Length`, which specifies the number of elements in the array. In addition, class `Array` provides `static` methods that provide algorithms for processing arrays. Typically, class `Array` overloads these methods—for example, `Array` method `Reverse` can reverse the order of the elements in an entire array or in a specified range of elements. For a complete list of class `Array`'s `static` methods visit

> https://msdn.microsoft.com/library/system.array

Figure 19.3 demonstrates several `static` methods of class `Array`.

```
```csharp
1  // Fig. 19.3: UsingArray.cs
2  // Array class static methods for common array manipulations.
3  using System;
4  using static System.Array;
```
```

**Fig. 19.3** | Array class static methods for common array manipulations. (Part 1 of 3.)

```
```csharp
using System.Collections;
// demonstrate algorithms of class Array
class UsingArray
{
    private static int[] intValues = {1, 2, 3, 4, 5, 6};
    private static double[] doubleValues = {8.4, 9.3, 0.2, 7.9, 3.4};
    private static int[] intValuesCopy;

    // method Main demonstrates class Array's methods
    static void Main()
    {
        intValuesCopy = new int[intValues.Length]; // defaults to zeroes

        Console.WriteLine("Initial array values:\n");
        PrintArrays(); // output initial array contents

        // sort doubleValues
        Sort(doubleValues); // unqualified call to Array static method Sort

        // copy intValues into intValuesCopy
        Array.Copy(intValues, intValuesCopy, intValues.Length);

        Console.WriteLine("\nArray values after Sort and Copy:\n");
        PrintArrays(); // output array contents
        Console.WriteLine();

        // search for 5 in intValues
        int result = Array.BinarySearch(intValues, 5);
        Console.WriteLine(result >= 0 ?
            "5 found at element {0} in intValues" :
            "5 not found in intValues");

        // search for 8763 in intValues
        result = Array.BinarySearch(intValues, 8763);
        Console.WriteLine(result >= 0 ?
            "8763 found at element {0} in intValues" :
            "8763 not found in intValues");
    }

    // output array content with enumerators
    private static void PrintArrays()
    {
        Console.Write("doubleValues: ");

        // iterate through the double array with an enumerator
        IEnumerator enumerator = doubleValues.GetEnumerator();

        while (enumerator.MoveNext())
        {
            Console.Write($"{enumerator.Current} ");
        }
    }
}
```
