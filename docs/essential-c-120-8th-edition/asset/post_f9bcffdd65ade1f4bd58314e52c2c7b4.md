
# Dictionary Collections: Dictionary<TKey, TValue>

Another category of collection classes is the dictionary classes—specifically, Dictionary<TKey, TValue> (see Figure 17.3). Unlike the collections, dictionary classes store name/value pairs. The name functions as a unique key that can be used to lookup the corresponding element in a manner similar to that of using a primary key to access a record in a database. This adds some complexity to the access of dictionary elements, but because lookups by key are efficient operations, this is a useful collection. Note that the key may be any data type, not just a string or a numeric value.

One option for inserting elements into a dictionary is to use the Add() method, passing both the key and the value as arguments, as shown in Listing 17.5.

Listing 17.5: Adding Items to a Dictionary<TKey, TValue>

```c
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        var colorMap = new Dictionary<string, ConsoleColor>
        {
            ["Error"] = ConsoleColor.Red,
            ["Warning"] = ConsoleColor.Yellow,
            ["Information"] = ConsoleColor.Green
        };
        colorMap.Add("Verbose", ConsoleColor.White);
        // ...
    }
}
```

After initializing the dictionary with a dictionary initializer³ (see the section “Collection Initializers” in Chapter 15), Listing 17.5 inserts the string ConsoleColor of White for the key of “Verbose”. If an element with the same key has already been added, an exception is thrown.

An alternative for adding elements is to use the indexer, as shown in Listing 17.6.

+ 3. Starting with C# 6.0.

IDictionary<TKey, TValue>
ICollection<KeyValuePair<TKey, TValue>>
IEnumerable<KeyValuePair<TKey, TValue>>
IDictionary
ICollection
IEnumerable
ISerializable
IDerializationCallback

# Dictionary<TKey, TValue> Generic Class

![](img/ffe0f34eac7523830420733690014d17_880_0.png)

FIGURE 17.3: Dictionary class diagrams

# LISTING 17.6: Inserting Items in a Dictionary<TKey, TValue> Using the Index Operator

```csharp
using System;
using System.Collections.Generic;

public class Program{
    public static void Main()
    {
        var colorMap = new Dictionary<string, ConsoleColor>{
            ["Error"] = ConsoleColor.Red,
            ["Warning"] = ConsoleColor.Yellow,
            ["Information"] = ConsoleColor.Green
        };
        colorMap["Verbose"] = ConsoleColor.White;
        colorMap["Error"] = ConsoleColor.Cyan;
        // ...
    }
}
```

The first thing to observe in Listing 17.6 is that the index operator does not require an integer. Instead, the index operand type is specified by the first argument (string), and the type of the value that is set or retrieved by the indexer is specified by the second type argument (ConsoleColor).

The second thing to notice in Listing 17.6 is that the same key "Error" is used twice. In the first assignment, no dictionary value corresponds to the given key. When this happens, the dictionary collection classes insert a new value with the supplied key. In the second assignment, an element with the specified key already exists. Instead of inserting an additional element, the prior ConsoleColor value for the "Error" is replaced with ConsoleColor.Cyan.

Attempting to read a value from a dictionary with a nonexistent key throws a NotFoundException. The ContainsKey() method allows you to check whether a particular key is used before accessing its value, thereby avoiding the exception.

The Dictionary<TKey, TValue> is implemented as a hash table; this data structure provides extremely fast access when searching by key, regardless of the number of values stored in the dictionary. By contrast, checking there is a particular value in the dictionary collections is a time-consuming operation with linear performance characteristics, like searching an unsorted list. To do this, you use the ContainsValue() method, which searches sequentially through each element in the collection.

Remove a dictionary element using the Remove() method, passing the key, not the element value, as the argument.

Because both the key and the value are required to add a value to the dictionary, the loop foreach variable elements of a dictionary must be KeyValuePair<TKey, TValue>. Listing 17.7 shows a snippet of code demonstrating the use of a foreach loop to enumerate the keys and values in a dictionary. The output appears in Output 17.3.

Listing 17.7: Iterating over Dictionary<TKey, TValue> with foreach

```csharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        var colMap = new Dictionary<string, ConsoleColor>
        {
            ["Error"] = ConsoleColor.Red,
            ["Warning"] = ConsoleColor.Yellow,
            ["Information"] = ConsoleColor.Green,
            ["Verbose"] = ConsoleColor.White
        };

        Print(colMap);
    }

    private static void Print(IEnumerable<KeyValuePair<string, ConsoleColor>> items)
    {
        foreach (KeyValuePair<string, ConsoleColor> item in items)
        {
            Console.ForegroundColor = item.Value;
            Console.WriteLine(item.Key);
        }
    }
}
```

# OUTPUT 17.3

```
Error
Warning
Information
Verbose
```

Note that the order of the items shown here is the order in which the items were added to the dictionary, just as if they had been added to a list. Implementations of dictionaries will often enumerate the keys and values in the order in which they were added to the dictionary, but this feature is neither nor documented, so you should not rely on it.

# Guidelines

> DO NOT make any unwarranted assumptions about the order in which elements of a collection will be enumerated. If the collection is not documented as enumerating its elements in a particular order, it is not guaranteed to produce elements in any particular order.

If you want to deal only with keys or only elements within a dictionary class, they are available via the Keys and Values properties, respectively. The data type returned from these properties is of type ICollection<T>. The data returned by these properties is a reference to the data within the original dictionary collection rather than a copy; changes within the dictionary are automatically reflected in the collection returned by the Keys and Values properties.

# ADVANCED TOPIC

# Customizing Dictionary Equality

To determine whether a given key matches any existing key in the dictionary, the dictionary must be able to compare two keys for equality. This is analogous to the way that lists must be able to compare two items to determine their order. (For an example, "Advanced Topic: Customizing Collection Sorting" earlier in this chapter.) By default, two instances of a value type are compared by checking whether they exactly contain the same data, and two instances of a reference type are compared to see whether both reference the same object. However, it is occasionally necessary to be able to compare two instances as equal if they are not exactly the same value or exactly the same reference.

For example, suppose you wish to create a Dictionary<Contact, string> using the Contact type from Listing 17.2. However, you want any two objects to compare as equal if they have the first and last names, regardless of whether the two objects are reference equal. Much as you can provide an implementation of IComparer<T> to sort a list, so you can provide an implementation of IEqualityComparer<T> to determine if two keys are equal: one returns whether two items are equal and one returns a "hash code" that the dictionary can use to facilitate fast indexing. Listing 17.8 shows an example.

# Listing 17.8: Implementing IComparer<T>

```csharp
using System.Collections.Generic;

public class ContactEquality : IComparer<Contact>
{
    public bool Equals(Contact x, Contact? y)
    {
        if(object.ReferenceEquals(x, y))
            return true;
        if(x == null || y == null)
            return false;
        return x.LastName == y.LastName &&
               x.FirstName == y.FirstName;
    }

    public int GetHashCode(Contact x)
    {
        if(x is null)
            return 0;

        int h1 = x.FirstName == null ? 0 : x.FirstName.GetHashCode();
        int h2 = x.LastName == null ? 0 : x.LastName.GetHashCode();
        return h1 * 23 + h2;
    }
}
```
