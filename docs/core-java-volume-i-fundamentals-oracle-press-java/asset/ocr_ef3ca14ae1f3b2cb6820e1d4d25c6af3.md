+   - `default boolean removeIf(Predicate<? super E> filter)` 8
+     removes all matching elements.

**`java.util.List<E>` 1.2**

+   - `default void replaceAll(UnaryOperator<E> op)` 8
+     applies the operation to all elements of this list.

# ### 9.6.5 Bulk Operations

There are several operations that copy or remove elements “in bulk.” The call

```
coll1.removeAll(coll2);
```

removes all elements from `coll1` that are present in `coll2`. Conversely,

```
coll1.retainAll(coll2);
```

removes all elements from `coll1` that are *not* present in `coll2`. Here is a typical application.

Suppose you want to find the *intersection* of two sets—the elements that two sets have in common. First, make a new set to hold the result.

```
var result = new HashSet<String>(firstSet);
```

Here, we use the fact that every collection has a constructor whose parameter is another collection that holds the initialization values.

Now, use the `retainAll` method: