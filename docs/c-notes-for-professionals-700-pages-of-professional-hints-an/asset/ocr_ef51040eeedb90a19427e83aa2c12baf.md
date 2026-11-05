# Section 66.48: Select with Func<TSource, int, TResult> selector - Use to get ranking of elements

On of the overloads of the SELECT extension methods also passes the index of the current item in the collection being SELECTed. These are a few uses of it.

# Get the "row number" of the items

```
var rowNumbers = collection.OrderBy(item => item.Property1)
    .ThenBy(item => item.Property2)
    .ThenByDescending(item => item.Property3)
    .Select((item, index) => new { Item = item, RowNumber = index })
    .ToList();
```

# Get the rank of an item within its group

```
var rankInGroup = collection.GroupBy(item => item.Property1)
    .OrderBy(group => group.Key)
    .SelectMany(group => group.OrderBy(item => item.Property2)
        .ThenByDescending(item => item.Property3)
        .Select((item, index) => new
        {
            Item = item,
            RankInGroup = index
        })).ToList();
```

# Get the ranking of groups (also known in Oracle as dense_rank)

```
var rankOfBelongingGroup = collection.GroupBy(item => item.Property1)
    .OrderBy(group => group.Key)
    .Select((group, index) => new
    {
        Items = group,
        Rank = index
    })
    .SelectMany(v => v.Items, (s, i) => new
    {
        Item = i,
        DenseRank = s.Rank
    }).ToList();
```

For testing this you can use:

```
public class SomeObject
{
    public int Property1 { get; set; }
    public int Property2 { get; set; }
    public int Property3 { get; set; }

    public override string ToString()
    {
        return string.Join(", ", Property1, Property2, Property3);
    }
}
```

And data:

```
List<SomeObject> collection = new List<SomeObject>
```