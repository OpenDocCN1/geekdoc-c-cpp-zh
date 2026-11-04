Notice that the string concatenation example is very inefficient due to the allocation of lots of intermediate strings for the partial results of the concatenation operation. It would be much better to use a StringBuilder for this, which can also be done using Aggregate:

```
new[] { 3, 7, 1, 5, 0, 8, 0, 4, 2 }
. Aggregate(new StringBuilder(), (sb, n) => sb.Append(n.ToString()))
```

The StringBuilder type has an Append method that appends the given string to the end of the buffer, returning the StringBuilder itself so one can continue appending things to it in a fluent manner. This time, the aggregation type is a StringBuilder, meaning the return type will be StringBuilder, too. Instead we likely want to transform this result into a string, which can be done by calling ToString on the result. Alternatively, an overload of Aggregate can be used to do this final transformation on the result:

```
R Aggregate<T, A, R>(this IEnumerable<T> source,
    A seed,
    Func<A, T, A> accumulate,
    Func<A, R> resultSelector);
```

In our example, we can use this overload to specify the final step of turning the used StringBuilder into a string:

```
new[] { 3, 7, 1, 5, 0, 8, 0, 4, 2 }
. Aggregate(new StringBuilder(),
    (sb, n) => sb.Append(n.ToString()),
    sb => sb.ToString())
```

# Count and LongCount

One of the simplest aggregation operations is counting the number of elements that occur in the source sequence. Count and LongCount do precisely that, respectively returning an Int32 and Int64 value. The signatures are shown here:

```
int Count<T>(this IEnumerable<T> source);
long LongCount<T>(this IEnumerable<T> source);
```

Based on the earlier discussion about Aggregate, it should be clear that the same effect can be achieved by relying on Aggregate, as follows:

```
source.Aggregate(0, (n, item) => n + 1)
```

The only slightly strange thing about this form of aggregation is that the elements from the input sequence are not being used in the aggregation result.