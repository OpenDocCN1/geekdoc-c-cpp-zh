items on the right sequence one must make sure that the object is not null before accessing its properties. Otherwise it will result in a NullReferenceException. Example:

```
var leftSequence = new List<int> { 1, 2, 5 };
var rightSequence = new List<dynamic>()
{
    new { Value = 1 },
    new { Value = 2 },
    new { Value = 3 },
    new { Value = 4 },
};

var numbersAsChars = (
    from l in leftSequence
    join r in rightSequence
    on l equals r.Value into leftJoin
    from result in leftJoin.DefaultIfEmpty()
    select new
    {
        Left = l,
        // 5 will not have a matching object in the right so result
        // will be equal to null.
        // To avoid an error use:
        //   - C# 6.0 or above - result?.Value
        //   - Under - result == null ? 0 : result.Value
        Right = result?.Value
    }).ToList();
```

# Section 66.36: ToDictionary

The ToDictionary() LINQ method can be used to generate a Dictionary<TKey, TElement> collection based on a given IEnumerable<T> source.

```
IEnumerable<User> users = GetUsers();
Dictionary<int, User> usersById = users.ToDictionary(x => x.Id);
```

In this example, the single argument passed to ToDictionary is of type Func<TSource, TKey>, which returns the key for each element.

This is a concise way to perform the following operation:

```
Dictionary<int, User> usersById = new Dictionary<int, User>();
foreach (User u in users)
{
    usersById.Add(u.Id, u);
}
```

You can also pass a second parameter to the ToDictionary method, which is of type Func<TSource, TElement> and returns the Value to be added for each entry.

```
IEnumerable<User> users = GetUsers();
Dictionary<int, string> userNamesById = users.ToDictionary(x => x.Id, x => x.Name);
```

It is also possible to specify the IComparer that is used to compare key values. This can be useful when the key is a string and you want it to match case-insensitive.

```
IEnumerable<User> users = GetUsers();
Dictionary<string, User> usersByCaseInsensitiveName = users.ToDictionary(x => x.Name,
```