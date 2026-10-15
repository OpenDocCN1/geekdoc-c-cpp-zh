given key. When this happens, the dictionary collection classes insert a new value with the supplied key. In the second assignment, an element with the specified key already exists. Instead of inserting an additional element, the prior ConsoleColor value for the “Error” key is replaced ConsoleColor.Cyan.

Attempting to read a value from a dictionary with a nonexistent key throws a KeyNotFoundException. The ContainsKey() method allows you to check whether a particular key is used before accessing its value, thereby avoiding the exception.

The Dictionary<TKey, TValue> is implemented as a “hash table”; this data structure provides extremely fast access when searching by key, regardless of the number of values stored in the dictionary. By contrast, checking whether there is a particular value in the dictionary collections is a time-consuming operation with linear performance characteristics, much like searching an unsorted list. To do this you use the ContainsValue() method, which searches sequentially through each element in the collection.

You remove a dictionary element using the Remove() method, passing the key, not the element value.

Because both the key and the value are required to add a value to the dictionary, the loop variable of a foreach loop that enumerates elements of a dictionary must be KeyValuePair<TKey, TValue>. Listing 16.7 shows a snippet of code demonstrating the use of a foreach loop to enumerate the keys and values in a dictionary. The output appears in Output 16.3.

# LISTING 16.7: Iterating over Dictionary<TKey, TValue> with foreach

```
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // C# 6.0 (use {"Error", ConsoleColor.Red} pre-C# 6.0)
        Dictionary<string, ConsoleColor> colorMap =
            new Dictionary<string, ConsoleColor>
            {
                ["Error"] = ConsoleColor.Red,
                ["Warning"] = ConsoleColor.Yellow,
                ["Information"] = ConsoleColor.Green,
                ["Verbose"] = ConsoleColor.White
            };

        Print(colorMap);
```