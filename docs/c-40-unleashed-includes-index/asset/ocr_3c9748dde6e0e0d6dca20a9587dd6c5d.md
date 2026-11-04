# DefaultIfEmpty

Where Empty sort of plays the role of a null reference, DefaultIfEmpty plays the role of the null coalescing ?? operator. If the sequence given to this operator is empty, it yield returns a single “default” element. This default element can either be specified explicitly or inferred based on the sequence's element type:

```
var src1 = Enumerable.Empty<int>();
var res1 = src1.DefaultIfEmpty(); // { 0 }
var res2 = src1.DefaultIfEmpty(99); // { 99 }

var src2 = Enumerable.Range(1, 9);
var res3 = src2.DefaultIfEmpty(); // { 1 .. 9 }
```

This operator has quite limited use, but it's nevertheless good to know about.

# Restriction

One of the most common query operations is obviously to filter out elements based on certain conditions. Those conditions can either be on a per-element basis (such as with the Where operator) or have a more global nature (as with Skip or Take). In essence, we're talking here about horizontal partitioning where a given number of objects in the input sequence are filtered down to a subset. Those restriction operators don't change the shape of the data and preserve the type of the input sequence.

# Where

The first restriction operator is one we're already familiar with. The Where operator evaluates a condition for each element in the input sequence, only retaining objects for which the condition evaluated to true. Two overloads exist:

```
static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, bool> predicate);
static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, int, bool> predicate);
```

From our discussion about query expression syntax and iterators, we remember the first one quite well. Iterating over the source parameter, the operator feeds every object in to the predicate function. When that function evaluates to true, it yields the object into the output sequence. Any Boolean-returning expression will do, no matter how complex you make it. For illustration purposes, we keep the predicate function simple:

```
// { "Bart", "Lisa" }
var res = new [] { "Bart", "Homer", "Lisa" }.Where(s => s.Length == 4);
```