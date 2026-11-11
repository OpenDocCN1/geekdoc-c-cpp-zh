# ✓ **TIP:**

You can avoid the cumbersome `Map.Entry` by using a var declaration.

```
```java
for (var entry : map.entrySet())
{
    do something with entry.getKey(), entry.getValue()
}
```
```

Or simply use the `forEach` method:

```
```java
map.forEach((k, v) ->
{
    do something with k, v
});
```
```

If you invoke the remove method of the iterator on the key set view, you actually remove the key *and its associated value* from the map. However, you cannot add an element to the key set view. It makes no sense to add a key without also adding a value. If you try to invoke the add method, it throws an `UnsupportedOperationException`. The entry set view has the same restriction, even though it would make conceptual sense to add a new key/value pair.

**java.util.Map<K, V>** 1.2

- `Set<Map.Entry<K, V>> entrySet()`  
  returns a set view of `Map.Entry` objects, the key/value pairs in the map. You can remove elements from this set and they are removed from the map, but you cannot add any elements.

- `Set<K> keySet()`  
  returns a set view of all keys in the map. You can remove elements from this set and the keys and associated values are removed from