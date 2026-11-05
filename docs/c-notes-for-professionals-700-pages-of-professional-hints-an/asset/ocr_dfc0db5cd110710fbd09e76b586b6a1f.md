```
StringComparer.InvariantCultureIgnoreCase);
var user1 = usersByCaseInsensitiveName["John"];
var user2 = usersByCaseInsensitiveName["JOHN"];
user1 == user2; // Returns true
```

Note: the ToDictionary method requires all keys to be unique, there must be no duplicate keys. If there are, then an exception is thrown: ArgumentException: An item with the same key has already been added. If you have a scenario where you know that you will have multiple elements with the same key, then you are better off using ToLookup instead.

# Section 66.37: Concat

Merges two collections (without removing duplicates)

```
List<int> foo = new List<int> { 1, 2, 3 };
List<int> bar = new List<int> { 3, 4, 5 };

// Through Enumerable static class
var result = Enumerable.Concat(foo, bar).ToList(); // 1,2,3,3,4,5

// Through extension method
var result = foo.Concat(bar).ToList(); // 1,2,3,3,4,5
```

# Section 66.38: Build your own Linq operators for IEnumerable<T>

One of the great things about Linq is that it is so easy to extend. You just need to create an extension method whose argument is IEnumerable<T>.

```
public namespace MyNamespace
{
    public static class LinqExtensions
    {
        public static IEnumerable<List<T>> Batch<T>(this IEnumerable<T> source, int batchSize)
        {
            var batch = new List<T>();
            foreach (T item in source)
            {
                batch.Add(item);
                if (batch.Count == batchSize)
                {
                    yield return batch;
                    batch = new List<T>();
                }
            }
            if (batch.Count > 0)
                yield return batch;
        }
    }
}
```

This example splits the items in an IEnumerable<T> into lists of a fixed size, the last list containing the remainder of the items. Notice how the object to which the extension method is applied is passed in (argument source) as the initial argument using the this keyword. Then the yield keyword is used to output the next item in the output IEnumerable<T> before continuing with execution from that point (see yield keyword).