distinct key value. The key value is determined by the "key selection" each expression, which is an expression that equates the key value for each element (c.state in the previous example). All source elements that equate to an equal key value using the key selection expression will be partitioned into the same group.

The GroupBy extension operator has many overloads; the simplest has a single key selection argument. The remaining overloads of this operator allow specific control over how element equality is evaluated, the select projection to use for the resulting groups, and what select projection is used for generating each element in any resulting group.

The following GroupBy extension method signature shows all of the possible arguments:

```
public static IEnumerable<TResult>
    GroupBy<TSource, TKey, TElement, TResult(
        IEnumerable<TSource> source,
        Func<TSource, TKey> keySelector,
        Func<TSource, TElement>
        elementSelector,
        Func<TKey, IEnumerable<TElement>, TResult>
        resultSelector,
        IEqualityComparer<TKey> compare
```

Independent from how the GroupBy projects the results, the resulting sequence exposes groups that have a common Key property value. The members of these groupings themselves can be enumerated to obtain the individual group elements.

SEQUENCE ORDERING The key order by default is the order each key value first appears in the source collection. If you want an alternative key order, sort the source collection first using the normal ordering operators.

# Working with Groups

The return collection from a GroupBy or group x by y query is

```
IEnumerable<IGrouping<TKey, TElement>>
```