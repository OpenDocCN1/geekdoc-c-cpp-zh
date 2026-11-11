```
```
map.forEach((k, v) -> {
    do something with k, v
});
```
```

If you invoke the `remove` method of the iterator on the key set view, you actually remove the *key and its associated value* from the map. However, you cannot *add* an element to the key set view. It makes no sense to add a key without also adding a value. If you try to invoke the *add* method, it throws an *UnsupportedOperationException*. The entry set view has the same restriction, even though it would make conceptual sense to add a new key/value pair.

`java.util.Map<K, V>` 1.2

+   - `Set<Map.Entry<K, V>> entrySet()`
+     returns a set view of Map.Entry objects, the key/value pairs in the map. You can remove elements from this set and they are removed from the map, but you cannot add any elements.
+   - `Set<K> keySet()`
+     returns a set view of all keys in the map. You can remove elements from this set and the keys and associated values are removed from the map, but you cannot add any elements.
+   - `Collection<V> values()`
+     returns a collection view of all values in the map. You can remove elements from this set and the removed value and its key are removed from the map, but you cannot add any elements.

`java.util.Map.Entry<K, V>` 1.2

+   - `K getKey()`
+   - `V getValue()`
+     returns the key or value of this entry.
+   - `V setValue(V newValue)`
+     changes the value *in the associated map* to the new value and returns the old value.

# ### 9.4.4 Weak Hash Maps

The collection class library has several map classes for specialized needs that we briefly discuss in this and the following sections.