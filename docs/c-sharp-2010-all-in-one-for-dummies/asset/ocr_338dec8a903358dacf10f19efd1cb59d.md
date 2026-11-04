of `_keys` corresponds to the ith entry of `_arrayElements`. The application program can then index `KeyedArray` via string identifiers that have meaning to the application.

![](bbox=[0.139, 0.196, 0.225, 0.27])

A noninteger index is referred to as a `key`. By the way, you can implement `KeyedArray` with an underlying `List<T>` instead of the fixed-size array. `List<T>` is indexable like an array because both implement the `IList` (or `IList<T>`) interface. This allows `KeyedArray` to be generic and to be much more flexible than using the integer array.

The `set[]` indexer starts by checking to see whether the specified index already exists by calling the method `Find()`. If `Find()` returns an index, `set[]` stores the new data object into the corresponding index in `_arrayElements`. If `Find()` can't find the key, `set[]` calls `FindEmpty()` to return an empty slot in which to store the object provided.

The `get[]` side of the index follows similar logic. It first searches for the specified key using the `Find()` method. If `Find()` returns a nonnegative index, `get[]` returns the corresponding member of `_arrayElements` where the data is stored. If `Find()` returns -1, `get[]` returns null, indicating that it can't find the provided key anywhere in the list.

The `Find()` method loops through the members of `_keys` to look for the element with the same value as the string `targetKey` passed in. `Find()` returns the index of the found element (or -1 if none was found). `FindEmpty()` returns the index of the first element that has no key element.

![](bbox=[0.139, 0.573, 0.226, 0.659])

Neither `Find()` nor `FindEmpty()` is written in an efficient manner. Any number of ways exist to make these methods faster, none of which has anything to do with indexers.

![](bbox=[0.123, 0.653, 0.226, 0.73])

Hey, wouldn't it be cool to provide an indexer for the `LinkedList` class? Sure, you can do that. But notice that even in `KeyedArray`, you must loop through the underlying `_keys` array to locate a specified key—which is why I provide `Find()` and `FindEmpty()`, which do just that. You would also have to implement an indexer for `LinkedList` by looping through the list, and the only way to do that is the same way you iterate it with `LinkedListIterator`—or by following the forward links from node to node. An indexer would be convenient but wouldn't speed things up.

![](bbox=[0.123, 0.782, 0.226, 0.87])

Notice that you can't remove an element by providing a null key. As they used to say in college textbooks, “This problem is left as an exercise for the reader.”