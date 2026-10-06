```
/* built-in string comparer statics are helpful.
* See the topic heading later in this chapter -
* Custom EqualityComparers When Using LINQ Set Operators
```

# Output 6-2

Distinct example: 1, 2, 3, 1, 2, 3, 4, 5 -
1 2 3 4 5

Distinct example: one, ONE, One, Two, Two
oneTwo

# Except Operator

The Except operator produces the set difference between two sequences.
It will only return elements in the first sequence that don't appear in the supplied
second sequence using either the default EqualityComparer or a supplied
EqualityComparer. It operates by first obtaining a distinct list of elements
in the second sequence and then iterating the first sequence and only
returns elements that do not appear in the second sequence's distinct list.
An ArgumentNullException is thrown if either collection is null when this
operator is called.

The method signatures available for the Except operator are:

```
// Returns the elements from the source sequence
// that are not in the second collection using
// EqualityComparer<TSource>.Default comparer to
// to compare elements.
// IEnumerable<TSource> Except<TSource>(
```