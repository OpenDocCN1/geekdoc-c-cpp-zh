# LISTING 17.5: Adding Items to a Dictionary<TKey, TValue>

```
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // C# 6.0 (use {"Error", ConsoleColor.Red} pre-C# 6.0)
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

After initializing the dictionary with a C# 6.0 dictionary initializer (see the section “Collection Initializers” in Chapter 15), Listing 17.5 inserts the string a ConsoleColor of white for the key of “Verbose”. If an element with the same key has already been added, an exception is thrown.

An alternative for adding elements is to use the indexer, as shown in Listing 17.6.

# LISTING 17.6: Inserting Items in a Dictionary<TKey, TValue> Using the Index Operator

```
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // C# 6.0 (use {"Error", ConsoleColor.Red} pre-C# 6.0)
        var colorMap = new Dictionary<string, ConsoleColor>
        {
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