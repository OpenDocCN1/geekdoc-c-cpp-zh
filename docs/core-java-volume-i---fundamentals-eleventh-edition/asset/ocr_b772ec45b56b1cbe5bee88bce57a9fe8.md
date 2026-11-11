# 9.4.7 Identity Hash Maps

The IdentityHashMap has a quite specialized purpose. Here, the hash values for the keys should not be computed by the hashCode method but by the System.identityHashCode method. That's the method that Object.hashCode uses to compute a hash code from the object's memory address. Also, for comparison of objects, the IdentityHashMap uses ==, not equals.

In other words, different key objects are considered distinct even if they have equal contents. This class is useful for implementing object traversal algorithms, such as object serialization, in which you want to keep track of which objects have already been traversed.

| `java.util.WeakHashMap<K, V> 1.2` |
| --- |
| • WeakHashMap()<br>• WeakHashMap(int initialCapacity)<br>• WeakHashMap(int initialCapacity, float loadFactor)<br>  constructs an empty hash map with the specified capacity and load factor. |

| `java.util.LinkedHashSet<E> 1.4` |
| --- |
| • LinkedHashSet()<br>• LinkedHashSet(int initialCapacity)<br>• LinkedHashSet(int initialCapacity, float loadFactor)<br>  constructs an empty linked hash set with the specified capacity and load factor. |

| `java.util.LinkedHashMap<K, V> 1.4` |
| --- |
| • LinkedHashMap()<br>• LinkedHashMap(int initialCapacity)<br>• LinkedHashMap(int initialCapacity, float loadFactor)<br>• LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder)<br>  constructs an empty linked hash map with the specified capacity, load factor, and ordering. The accessOrder parameter is true for access order, false for insertion order. |

*(Continues)*