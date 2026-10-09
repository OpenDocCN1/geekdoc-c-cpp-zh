# **LISTING 17.1: Using List<T>**

```
```
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<string> list = new List<string>();

        // Lists automatically expand as elements
        // are added
        list.Add("Sneezy");
        list.Add("Happy");
        list.Add("Dopecy");
        list.Add("Doc");
        list.Add("Sleepy");
        list.Add("Bashful");
        list.Add("Grumpy");

        list.Sort();

        Console.WriteLine(
            $"In alphabetical order { list[0] } is the "
            + $"first dwarf while { list[6] } is the last.");

        list.Remove("Grumpy");
    }
}
```
```

# **OUTPUT 17.1**

> In alphabetical order Bashful is the first dwarf while Sneezy is the last.

C# is zero-index based; therefore, index 0 in Listing 17.1 corresponds to the first element and index 6 indicates the seventh element. Retrieving elements by index does not involve a search. Rather, it entails a quick and simple “jump” operation to a location in memory.

A List<T> is an ordered collection; the Add() method appends the given item to the end of the list. Before the call to Sort() in Listing 17.1, "Sneezy" was first and "Grumpy" was last; after the call, the list is sorted into alphabetical order rather than the order in which items were added. Some collections automatically sort elements as they are added, but List<T> is not one of them; an explicit call to Sort() is required for the elements to be sorted.