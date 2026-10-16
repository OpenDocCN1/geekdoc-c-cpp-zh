to access an element based on a key. Dictionaries are also known as hash tables or maps. The main feature of dictionaries is fast lookup based on keys. You can also add and remove items freely, a bit like a List<T>, but without the performance overhead of having to shift subsequent items in memory.

Figure 11.5 shows a simplified representation of a dictionary. Here employee-ids such as B4711 are the keys added to the dictionary. The key is transformed into a hash. With the hash a number is created to associate an index with the values. The index then contains a link to the value. The figure is simplified because it is possible for a single index entry to be associated with multiple values, and the index can be stored as a tree.

![](bbox=[0.1, 0.29, 0.9, 0.65])

# Figure 11.5

The .NET Framework offers several dictionary classes. The main class you use is Dictionary<TKey, TValue>.

# Dictionary Initializers

C# 6 defines a new syntax to initialize dictionaries at declaration. A dictionary with a key of int and a value of string can be initialized as follows:

```
var dict = new Dictionary<int, string>()
{
    [3] ="three",
    [7] ="seven"
};
```

Here, two elements are added to the dictionary. The first element has a