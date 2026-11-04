```
```csharp
static IEnumerable<T> OrderBy<T, K>(
    this IEnumerable<T> source,
    Func<T, K> keySelector);

static IEnumerable<T> OrderBy<T, K>(
    this IEnumerable<T> source,
    Func<T, K> keySelector,
    IComparer<K> comparer);
```
```

Their use should be self-explanatory. Notice, though, there’s no overload that omits the use of a key selector function, but you can always use the identity function to achieve that effect:

```
```csharp
// Same as    from x in new[] { 5, 2, 6, 3, 4, 1 }
//            orderby x
//            select x
var oneToSix = new[] { 5, 2, 6, 3, 4, 1 }.OrderBy(x => x) // { 1, 2, 3, 4, 5, 6 }
```
```

# ThenBy and ThenByDescending

After establishing a primary ordering, further orderings can be established using the family of ThenBy operators. In query expressions, the commas used in the comma-separated list of ordering keys correspond to ThenBy or ThenByDescending calls.

Additional overloads with a comparer object are available, but they don’t have a query expression syntax. The signatures are the same as the ones shown earlier for OrderBy operators.

# Grouping and Joining

Slightly more complex query functionality exists in the family of grouping and joining operators. The number of overloads for those standard query operators may be frightening at first, so let’s take a closer look.

# GroupBy

To put elements in buckets with similar properties, grouping operations are used. No fewer than eight overloads exist for the GroupBy operator, which by themselves can be grouped into some categories. One set of overloads exposes a sequence containing IGrouping<K,T> objects, which contain the grouping key and the elements that go with it (because each grouping object is also an IEnumerable):

```
```csharp
public interface IGrouping<TKey, TElement> : IEnumerable<TElement> {
    TKey Key { get; }
}
```
```