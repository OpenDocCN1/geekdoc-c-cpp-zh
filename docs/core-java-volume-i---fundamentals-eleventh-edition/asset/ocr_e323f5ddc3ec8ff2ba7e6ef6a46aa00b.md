# java.util.List 1.2

+   - `static <E> List<E> of()` 9
+   - `static <E> List<E> of(E e1)` 9
+   - ...
+   - `static <E> List<E> of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9, E e10)` 9
+   - `static <E> List<E> of(E... elements)` 9

yields an immutable list of the given elements, which must not be null.

# java.util.Set 1.2

+   - `static <E> Set<E> of()` 9
+   - `static <E> Set<E> of(E e1)` 9
+   - ...
+   - `static <E> Set<E> of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9, E e10)` 9
+   - `static <E> Set<E> of(E... elements)` 9

yields an immutable set of the given elements, which must not be null.

# java.util.Map 1.2

+   - `static <K, V> Map<K, V> of()` 9
+   - `static <K, V> Map<K, V> of(K k1, V v1)` 9
+   - ...
+   - `static <K,V> Map<K,V> of(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8, K k9, V v9, K k10, V v10)` 9

yields an immutable map of the given keys and values, which must not be null.

+   - `static <K,V> Map.Entry<K, V> entry(K k, V v)` 9

yields an immutable map entry of the given key and value, which must not be null.

+   - `static <K,V> Map<K, V> ofEntries(Map.Entry<? extends K, ? extends V>... entries)` 9

yields an immutable map of the given entries.