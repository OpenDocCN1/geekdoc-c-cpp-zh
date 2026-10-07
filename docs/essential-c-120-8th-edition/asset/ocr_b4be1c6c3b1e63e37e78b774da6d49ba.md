# Chapter 15: Collection Interfaces with Standard Query Operators

LISTING 15.10: Filtering with System.Linq.Enumerable.Where()

```
using System;
using System.Collections.Generic;
using System.Linq;
```

```
public class Program
{
    public static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        patents = patents.Where(
            patent -> patent.YearOfPublication.StartsWith("18"));
        Print(patents);
    }
    }
}
```

# OUTPUT 15.2

| Phonograph (1877)
Kinetoscope (1888)
Electrical Telegraph (1837)
Steam Locomotive (1815) |

Notice that the code assigns the output of the Where() call back to IEnumerable<T>. In other words, the output of IEnumerable<T>.Where() is a new IEnumerable<T> collection. In Listing 15.10, it is IEnumerable<Patent>.

Less obvious is that the Where() expression argument has not necessarily executed at assignment time. This is true for many of the standard query operators. In the case of Where(), for example, the expression is passed into the collection and “saved” not executed. Instead, the execution occurs only when it is necessary to begin iterating over the items within the collection. For example, a foreach loop, such as the one in Print() (in Listing 15.9), can trigger the expression to be evaluated for each item within the collection. At least conceptually, the Where() method should be understood as a means of specifying the query regarding what appears in the collection, not the actual work involved with iterating over the items to produce a new collection with potentially fewer items.