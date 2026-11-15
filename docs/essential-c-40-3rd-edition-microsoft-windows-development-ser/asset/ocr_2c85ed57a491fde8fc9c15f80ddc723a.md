# IList<T> versus IDictionary<TKey, TValue>

In a sense, lists are just the special case of dictionaries where the “key” is always an integer, and the key set is always a contiguous set of non-negative integers starting with zero. But that is a strong enough difference that it is worth having an entirely different class to represent it. When selecting a collection class, the first two interfaces to look for are `IList<T>` and `IDictionary<TKey, TValue>`. These interfaces determine whether the collection type is focused on retrieval via index or retrieval via key. If the type of collection you are using should be key-centric, use a collection class that implements the `IDictionary<TKey, TValue>` interface. Alternatively, the `IList<T>` interface provides support for element retrieval via index. In other words, although both of these interfaces require that the indexer be implemented, the implementations are fundamentally different. In the case of `IList<T>`, the parameter passed to the array operator corresponds to the index of the element being retrieved, the *nth* element in the list. In the case of the `IDictionary<TKey, TValue>` interface, the parameter corresponds to the key of a previously inserted element. When you assign using the key, a new item will be inserted if one doesn’t already exist for the specified key.

# IComparable<T>

Before I discuss the next interface in Figure 16.1, I need to discuss an interface that does not appear in the diagram but is nonetheless important to both `IList<T>` and `IDictionary<TKey, TValue>`. The `IComparable<T>` interface is crucial for any sorting operation by classes implementing these interfaces. For example, if the `List<T>.Sort()` method is called, you need a means to compare objects to determine their order. One way to do this is via the `IComparable<T>` interface. This interface has one method, `CompareTo()`. It returns an integer indicating whether the element passed is greater than, less than, or equal to the current element. For this to work the key data type needs to implement `IComparable<T>`.

# ADVANCED TOPIC

# Using IComparer<T> for Sorting

Another way to handle custom sorting is to pass an element that implements `IComparer<T>` into the sort method. This interface performs a function similar