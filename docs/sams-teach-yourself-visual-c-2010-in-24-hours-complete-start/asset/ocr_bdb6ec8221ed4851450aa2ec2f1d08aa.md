```
```text
yield return 4;
yield return 6;
yield return 8;
}

static void Main()
{
foreach(int i in GetEvenNumbers())
{
Console.WriteLine(i);
}
}
```
```

Iterators can do much more than simply yield values. As long as you abide by the restrictions previously mentioned, iterators can have any degree of sophistication in how they determine the values to yield. Listing 9.8 produces the same output as that from Listing 9.7 but does so using a more complex iterator.

# LISTING 9.8 A More Complex Iterator

```
```text
class Program
{
static IEnumerable<int> GetEvenNumbers()
{
for (int i = 0; i <= 9; i++)
{
if (i % 2 == 0)
{
yield return i;
}
}
}

static void Main()
{
foreach(int i in GetEvenNumbers())
{
Console.WriteLine(i);
}
}
}
```
```

# Summary

In this hour, you have learned how to work with large amounts of data using arrays and collections. Arrays are the simplest type of collection and have direct language support, whereas the other collection types, such as List<T> and Stack<T>, offer more flexibility and enable you to create your own specialized collections. You also learned how indexers enable your own classes to provide the same type of