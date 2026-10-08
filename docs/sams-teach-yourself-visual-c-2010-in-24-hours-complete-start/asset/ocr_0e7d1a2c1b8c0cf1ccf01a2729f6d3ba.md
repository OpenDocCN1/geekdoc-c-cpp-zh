# TABLE 9.5 Common Members of ReadOnlyCollection<T>

| Name | Description |
|---|---|
| Count | Gets the number of elements actually contained in the collection |
| Contains | Determines whether an element is in the collection |
| IndexOf | Searches for the specified element and returns the index of the first occurrence |

```
**ReadOnlyCollection<T>**

You can think of ReadOnlyCollection<T> as a wrapper around an existing mutable collection, which throws exceptions if you try to change it. The underlying collection is still mutable.
```

![](bbox=[0.81, 0.3, 0.96, 0.34])

# Dictionaries

List<T> and Collection<T> are useful for general purpose collections, but sometimes it is necessary to have a collection that can provide a mapping between a set of keys and a set of values, not allowing duplicate keys.

The Dictionary<TKey, TValue> class provides such a mapping and enables access using the key rather than a numeric index. To add an element to a Dictionary<TKey, TValue> instance, you must provide both a key and a value. The key must be unique and cannot be null, but if TValue is a reference type, the value can be null. Table 9.6 shows the common members of the Dictionary<TKey, TValue> class.

# TABLE 9.6 Common Members of Dictionary<TKey, TValue>

| Name | Description |
|---|---|
| Count | Gets the number of key/value pairs contained in the dictionary |
| Keys | Gets a collection containing the keys in the dictionary |
| Values | Gets a collection containing the values in the dictionary |
| Add | Adds the specified key and value to the dictionary |
| Clear | Removes all keys and values from the dictionary |
| ContainsKey | Determines if the dictionary contains the specified key |
| ContainsValue | Determines if the dictionary contains a specific value |
| Remove | Removes the value with the specified key from the dictionary |