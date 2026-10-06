# HOW TO GROUP ELEMENTS

IGrouping interface inherits from IEnumerable<TElement> (making itself enumerable) and exposes a Key property that indicates the unique result that formed this grouping. This interface has the following form:

```
public interface IGrouping<TKey, TElmt> : IEnumerable<TElmt>
{
    TKey Key { get; }
}
```

LINQ to Objects returns by default an internal class implementation of IGrouping<TKey, Element>, called Grouping. It is exposed via the IGrouping interface through the extension method signatures so that Microsoft can develop this over time. The only property you should rely on is the Key property. Most methods on the underlying grouping collection type throw a NotSupportedException and should be avoided.

Enumerating over the result of a GroupBy extension method or group x by y query expression yields IGrouping<TKey, TElement> element unique key. Each group instance has the mandatory Key property, and each group can be iterated to get the elements in that group.

The normal pattern for working with groups once they are generated is to use a nested foreach loop; the first enumerates the groups, and then an inner loop iterates the elements. The general pattern is

```
foreach (var group in q)
{
    // Group specific code here
    Console.WriteLine("Group key: {0}", group.Key);

    foreach (var element in group)
    {
        // Element specific code here
        Console.WriteLine(" - {0}*", element);
    }
n
```

# Specifying a Key to Group By

During evaluation, all elements that share common key values as evaluated by the keySelector expression will be grouped. Value equality is determined using the default Equals operator, although this behavior can be overridden by specifying a custom equality comparison function, as seen shortly.