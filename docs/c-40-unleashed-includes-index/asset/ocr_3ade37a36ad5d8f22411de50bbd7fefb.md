It’s left as an exercise for you to implement those operators by hand using your acquired knowledge of iterators. You’ll find that query operators are often just a few lines of code (ignoring input validation logic).

# Take and TakeWhile

The opposite of “to skip” is “to take,” returning a sequence with elements from the beginning of the input sequence, either based on a count or a condition. Take simply takes a number of elements to yield, while TakeWhile expresses “yield as long as the condition holds.” Examples are shown here:

```
var res1 = Enumerable.Range(0, 10).Take(5); // { 0, 1, 2, 3, 4 }
var res2 = Enumerable.Range(0, 10).TakeWhile(n => n < 8);
    // { 0, 1, 2, 3, 4, 5, 6, 7 }
```

Notice certain invariant properties hold. We demonstrate those in the following example using the Concat and SequenceEqual operators, which should be straightforward to understand. Both methods should return true every time:

```
bool AssertSkipTake<T>(IEnumerable<T> source, int n) {
    return source.SequenceEqual(source.Take(n).Concat(
        source.Skip(n)));
}
```

```
bool AssertSkipTakeWhile<T>(IEnumerable<T> source, Func<T, bool> predicate) {
    return source.SequenceEqual(source.TakeWhile(predicate).Concat(
        source.SkipWhile(predicate)));
}
```

# PAGING USE SKIP AND TAKE

The combination of Skip and Take is useful for paging of data sources (for example, to show elements ten at a time):

```
// For example, page 3 = Skip(30).Take(10)
var onePageOfData = source.Skip(page * pageSize).Take(pageSize);
```

This illustrates the power of gluing together different query operators.

# First and FirstOrDefault

Very restrictive restriction operators return just a single element. First is one of those operators, returning the first element of a sequence. If no element is present, it throws an InvalidOperationException. You can use the FirstOrDefault operator to return the default value for the sequence element type in case the input sequence is empty:

```
int first = new [] { 42, 24, 12, 123 }.First(); // 42
int zero  = new int[0].FirstOrDefault();
```