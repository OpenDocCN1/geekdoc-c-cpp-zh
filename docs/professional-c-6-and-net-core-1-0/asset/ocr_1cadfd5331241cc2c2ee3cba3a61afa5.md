System.Collections.Immutable offers some more immutable collection types as shown in the following table:

| Immutable Type | Description |
|---|---|
| ImmutableArray<T> | ImmutableArray<T> is a struct that uses an array type internally but doesn’t allow changes to the underlying type. This struct implements the interface IImmutableList<T>. |
| ImmutableList<T> | ImmutableList<T> uses a binary tree internally to map the objects and implements the interface IImmutableList<T>. |
| ImmutableQueue<T> | ImmutableQueue<T> implements the interface IImmutableQueue<T> that allows access to elements first-in-first-out with Enqueue, Dequeue, and Peek. |
| ImmutableStack<T> | ImmutableStack<T> implements the interface IImmutableStack<T> that allows access to elements first-in-last-out with Push, Pop, and Peek. |
| ImmutableDictionary<TKey, TValue> | ImmutableDictionary<TKey, TValue> is an immutable collection with unordered key/value pair elements implementing the interface IImmutableDictionary<TKey, TValue>. |
| ImmutableSortedDictionary<TKey, TValue> | ImmutableSortedDictionary<TKey, TValue> is an immutable collection with ordered key/value pair elements implementing the interface IImmutableDictionary<TKey, TValue>. |
| ImmutableHashSet<T> | ImmutableHashSet<T> is an immutable unordered hash set implementing the interface IImmutableSet<T>. This interface offers set functionality explained in Chapter 11. |
| ImmutableSortedSet<T> | ImmutableSortedSet<T> is an immutable ordered set implementing the interface IImmutableSet<T>. |