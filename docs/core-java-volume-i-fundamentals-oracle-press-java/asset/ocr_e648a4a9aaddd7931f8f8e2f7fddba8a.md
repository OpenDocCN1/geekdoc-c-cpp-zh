enumerated type.” All enumerated types extend the generic `Enum` class. For example, `Weekday` extends `Enum<Weekday>`.

# **9.4.7 Identity Hash Maps**

The `IdentityHashMap` has a quite specialized purpose. Here, the hash values for the keys should not be computed by the `hashCode` method but by the `system.identityHashCode` method. That’s the method that `object.hashCode` uses to compute a hash code from the object’s memory address. Also, for comparison of objects, the `IdentityHashMap` uses `==`, not `equals`.

In other words, different key objects are considered distinct even if they have equal contents. This class is useful for implementing object traversal algorithms, such as object serialization, in which you want to keep track of which objects have already been traversed.

**java.util.WeakHashMap<K, V>** 1.2

- `WeakHashMap()`
- `WeakHashMap(int initialCapacity)`
- `WeakHashMap(int initialCapacity, float loadFactor)`
  constructs an empty hash map with the specified capacity and load factor.

**java.util.LinkedHashSet<E>** 1.4

- `LinkedHashSet()`
- `LinkedHashSet(int initialCapacity)`
- `LinkedHashSet(int initialCapacity, float loadFactor)`