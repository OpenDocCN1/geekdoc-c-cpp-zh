# OUTPUT 14.3

```
Phonograph (1877)
Kinetoscope (1888)
Electrical Telegraph (1837)
Steam Locomotive (1815)
```

Notice that the code assigns the output of the Where() call back to IEnumerable<T>. In other words, the output of IEnumerable<T>.Where() is a new IEnumerable<T> collection. In Listing 14.13, it is IEnumerable<Patent>.

Less obvious is that the Where() expression argument has not necessarily been executed at assignment time. This is true for many of the standard query operators. In the case of Where(), for example, the expression is passed in to the collection and “saved” but not executed. Instead, execution of the expression occurs only when it is necessary to begin iterating over the items within the collection. A foreach loop, for example, such as the one in Print() (in Listing 14.12), will trigger the expression to be evaluated for each item within the collection. At least conceptually, the Where() method should be understood as a means of specifying the query regarding what appears in the collection, not the actual work involved with iterating over to produce a new collection with potentially fewer items.

# Projecting with Select()

Since the output from the IEnumerable<T>.Where() method is a new IEnumerable<T> collection, it is possible to again call a standard query operator on the same collection. For example, rather than just filtering the data from the original collection, we could transform the data (see Listing 14.14).

# LISTING 14.14: Projection with System.Linq.Enumerable.Select()

```
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        IEnumerable<Patent> patentsOf1800 = patents.Where(
            patent => patent.YearOfPublication.StartsWith("18"));
        IEnumerable<string> items = patentsOf1800.Select(
            patent => patent.ToString());
```