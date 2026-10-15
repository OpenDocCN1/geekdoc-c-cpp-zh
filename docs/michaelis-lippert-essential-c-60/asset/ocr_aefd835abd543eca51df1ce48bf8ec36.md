# OUTPUT 15.8

```
Aggregate, All, Any, AsEnumerable, Average, Cast, Concat, Contains,
Count, DefaultIfEmpty, Distinct, ElementAt, ElementAtOrDefault,
Empty, Except, First, FirstOrDefault, GroupBy, GroupJoin,
Intersect, Join, Last, LastOrDefault, LongCount, Max, Min, OfType,
OrderBy, OrderByDescending, Range, Repeat, Reverse, Select,
SelectMany, SequenceEqual, Single, SingleOrDefault, Skip,
SkipWhile, Sum, Take, TakeWhile, ThenBy, ThenByDescending, ToArray,
ToDictionary, ToList, ToLookup, Union, Where, Zip,
```

In this example, typeof(Enumerable).GetMembers() returns a list of all the members (methods, properties, and so on) on System.Linq.Enumerable. However, many of these members are overloaded, sometimes more than once. Rather than displaying the same member multiple times, Distinct() is called from the query expression. This eliminates the duplicate names from the list. (We cover the details of typeof() and reflection [where methods like GetMembers() are available] in Chapter 17.)

# Query Expressions Are Just Method Invocations

Somewhat surprisingly, adding query expressions to C# 3.0 required no changes to the CLR or to the CIL language. Rather, the C# compiler simply translates query expressions into a series of method calls. Consider, for example, the query expression from Listing 15.1, a portion of which appears in Listing 15.16.

# LISTING 15.16: Simple Query Expression

```
private static void ShowContextualKeywords1()
{
    IEnumerable<string> selection =
        from word in Keywords
        where word.Contains('*')
        select word;
    // ...
}
// ...
```

After compilation, the expression from Listing 15.16 is converted to an IEnumerable<T> extension method call from System.Linq.Enumerable, as shown in Listing 15.17.