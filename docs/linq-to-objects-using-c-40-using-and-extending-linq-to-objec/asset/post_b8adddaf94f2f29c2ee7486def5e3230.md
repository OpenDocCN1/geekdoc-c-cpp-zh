
elements-lements as it returns resulting elements. This operator is covered in more detail in Chapter 6, "Working with Set Data," when its use in set operations is explored.

The Distinct operator is not supported in the query expression syntax, so it is often appended to the end of a query using extension method syntax. To demonstrate how it is used, the following code removes duplicate strings. The Console output from this code is

Peter
Paul
Mary
Janet

```cs
string[] names = new string[] { "Peter", "Paul",
"Mary", "Paul", "Mary", "Janet" };
```

```cs
var q = (from s in names
      where s.Length > 3
      select s.Distinct());
```

```cs
foreach (var name in q)
    Console.WriteLine(name);
```

## How to Sort the Results

LINQ to Objects has comprehensive support for ordering and sorting results. Whether you need to sort in ascending order, descending order using different property values in any sequence, or all the way to write a specific ordering algorithm of your own, LINQ's sorting features can accommodate the full range of ordering requirements.

## Basic Sorting Syntax

The resulting collection of results from a query can be sorted in any desired fashion, considering culture and case sensitivity. When querying using extension method syntax, the OrderBy, OrderDescending, ThenBy, and ThenByDescending standard query operators manage this process. The OrderBy and ThenBy operators sort in an ascending order (for example, a to z), and the OrderDescending and ThenByDescending operators in descending order (z to a). Only the first sorting extension can use the OrderBy operators, and each subsequent sorting extension must use the ThenBy operators, of which there can be zero or many depending on how much control you want over the subsorting when multiple elements share equal order after the previous expressions.

The following examples demonstrate sorting a source sequence first by the w key, then in descending order by the x key, and then in ascending order by the y key:

```cs
source.OrderBy(w => w)
      .ThenByDescending(x => x)
      .ThenBy(y => y);
```

When using the query expression syntax, each sorting key and the optional direction keyword needs be separated by a comma. If the descending or ascending keywords are not specified, LINQ assumes ascending order. The result from ordering a collection will be an IEnumerable<T>, which allows further query operations to be cascaded end-to-end.

```cs
from v in source
orderby w, descending x, y
```

The ordering extension methods are implemented using a basic but efficient Quicksort algorithm (see http://en.wikipedia.org/wiki/Quicksort for further explanation of how this algorithm works). The implementation LINQ to Objects uses a sorting type called unstable, which simply means that elements with equal values may not retain their relative positions to the source (although this is solved by cascading the result into ThenBy or ThenByDescending operators). The algorithm is fairly fast, and lends itself to parallelization, which is certainly leveraged by Microsoft's investment in Parallel LINQ.

## What Is Parallelization?

Parallelization refers to improving performance of applications by fully leveraging multiple processors. Parallelization code demonstrates how LINQ queries can benefit from multicore and multiprocessor hardware improvements.

## Reversing the Order of a Result Sequence (Reverse)

Another ordering extension method that reverses an entire sequence is the Reverse operator. An important point when using Reverse operator is that it doesn't test the equality of elements or carry out any sorting; it simply returns elements starting from the last element, back to the first. The order returned will be the exact reciprocal of the order that have returned from the result sequence. The following example demonstrates Reverse operator, returning AC in the Console window:

```cs
string[] letters = new string[] { "C", "A" };
var q = letters.Reverse();
foreach (string s in q)
    Console.Write(" " + s);
```

## Case Insensitive and Cultural-specific String Ordering

Any standard query operator that involves sorting allows a specific comparer function to be supplied (when written using extension method syntax). The .NET class libraries contain a handy class called StringComparer, which has a set of predefined static comparers ready for use. The comparers allow us to alter string sorting behavior, controlling case-sensitivity and culture (the language setting for the current thread). Table 3-2 lists the StringComparer instances that can be used in any OrderBy or ThenBy query operator. (In addition, see the "Custom Comparers When Using LINQ Operators" section in Chapter 6, which is specifically about built-in string comparers and custom comparers.)

### The Built-in StringComparer Functions to Control Case Sensitivity and Culture-aware String Ordering

| Comparator | Description |
| :--- | :--- |
| CurrentCulture | Performs a case-sensitive string comparison using the word comparison rules of the current culture. |
| CurrentCultureIgnoreCase | Performs case-insensitive string comparisons using the word comparison rules of the current culture. |

**Table 3-2** The Built-in StringComparer Functions to Control Case Sensitivity and Culture-aware String Ordering

| Comparator | Description |
| :--- | :--- |
| InvariantCulture | Performs a case-sensitive string comparison using the word comparison rules of the invariant culture. |
| InvariantCultureIgnoreCase | Performs a case-insensitive string comparison using the word comparison rules of the invariant culture. |
| Ordinal | Performs a case-sensitive ordinal string comparison. |
| OrdinalIgnoreCase | Performs a case-insensitive ordinal string comparison. |

Listing 3-10 demonstrates the syntax and effect of using built-in string comparer instances offered by the .NET Framework. The Console output is shown in Output 3-7, where the default case-sensitive result can be forced to case-insensitive.

**Listing 3-10** Case and culture sensitive/insensitive ordering using StringComparer functions—see Output 3-7

```cs
string[] words = new string[] {
    "Janet", "Janet", "janet", "Janet" 
};

var cs = words.OrderBy(w => w);
var ci = words.OrderBy(w => w,
    StringComparer.CurrentCultureIgnoreCase);

Console.WriteLine("Original:");
foreach (string s in cs)
    Console.WriteLine(" " + s);

Console.WriteLine("Case Sensitive (default):");
foreach (string s in cs)
    Console.WriteLine(" " + s);

Console.WriteLine("Case Insensitive:");
foreach (string s in ci)
    Console.WriteLine(" " + s);
```

## Output 3-7

Original:
jANet
JANet
jan
Janet

Case Sensitive (default):
jan
JANet
Janet
Janet

Case Insensitive:
jan
JANet
jan
Janet

## Specifying Your Own Custom Sort Comparison Function

To support any sorting order that might be required, custom sort comparison classes are easy to specify. A custom compare class is a class based on a standard .NET Interface called IComparer<T>, which exposes a single method: Compare. This interface is not specifically for LINQ; it is the basis for all .NET Framework classes that require sorting (or custom sorting) capabilities.

Comparer works by returning an integer result, indicating the relationship between a pair of instance types. If the types are deemed equal, the function returns zero. If the first instance is less than the second instance, a negative value is returned, or if the first instance is larger than the second instance, the function returns a positive value. How you equate the integer result value is up to you.

To demonstrate a custom IComparer<>, Listing a comparison function that simply shuffles (in a random fashion) the input source. The algorithm simply makes a random choice as to whether two elements are less than or greater than each other. Output 3-8 shows the Console output from a simple sort of a source of strings in an array, although this result will be different (potentially) each time this code is executed.
