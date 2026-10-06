# 288 CHAPTER 9 PARALLEL LINQ TO OBJECTS

Microsoft decided to make this condition obsolete by marking the overload taking the second data source of IEnumerable<T> with an [Obsolete] attribute and throwing a System.NotSupportedException when called; the method signatures are shown in Listing 9-6. This messaging is intended to help the developers understand what they need to do in order to parallelize these operators.

# Listing 9-6 Calling binary operators with Parallel LINQ requires that both sources are ParallelQuery<T> types

```
[Obsolete("...")]
public static ParallelQuery<TSource> Concat<TSource(
    this ParallelQuery<TSource> first,
    IEnumerable<TSource> second);
```

```
public static ParallelQuery<TSource> Concat<TSource>(n    this ParallelQuery<TSource> first,
    ParallelQuery<TSource> second);
```

Listing 9-7 demonstrates how to correctly call a binary operator using ParallelQuery collections as the two input sources and shows the error message displayed when both sources aren't of ParallelQuery type.

# Listing 9-7 Using binary operators with Parallel LINQ

```
var source1 = new int[] { 1,2,3,4,5 };
var source2 = new int[] { 6,7,8,9,10 };
```

```
// ERROR - Obsolete warning
// The second data source of a binary operator must be
// of type System.Linq.ParallelQuery<T> rather than
// System.Collections.Generic.IEnumerable<T>.
// To fix this problem, use the AsParallel() extension
// method to convert the data source to
// System.Linq.ParallelQuery<T>.*
```

```
var q = source1.AsParallel().Concat(source2);
```

```
// the following queries work fine.
// remember to force ordering where appropriate.
var q1 = source1.AsParallel()
    .Concat(source2.AsParallel());
```

```
var q2 = source1.AsParallel().AsOrdered()
    .Concat(source2.AsParallel());
```