# 27.4 The IList Interface

The generic interface IList<T> extends IList<T> and describes lists with elements of type T. It has the following members in addition to ICollection<T>:

+   - Read-index(int i) returns or sets list number i, counting from 0. Throws ArgumentOutOfRangeException if i<0 or i=Count. Throws NotSupportedException if used to set an element on a read-only list.
- void Add(T x) adds element x at the end of the list.
- int IndexOf(T x) returns the position whose element equals x, if any; otherwise -1.
- void Insert(int i, T x) inserts x at position i. Existing elements at position i and have their position decremented by 1. Throws ArgumentOutOfRangeException if i<0 or i>Count. Throws NotSupportedException if the list is read-only.
- bool Remove(T x) removes the first element of the list that equals x, if any. Returns true if an element was removed. All elements at higher positions have moved by 1. Throws NotSupportedException if the list is read-only.
- void RemoveAt(int i) removes the element at index i. All elements at higher positions have their position decremented by 1. Throws ArgumentOutOfRangeException if i<0 or i=Count. Throws NotSupportedException if the list is read-only.

IList<T> is implemented by class List<T> which represents a list using an array (27.6).

# 27.5 The Dictionary<K,V> Interface

The generic interface Dictionary<K,V> extends ICollection<KeyValuePair<K,V>>, so it can be seen as a collection of key/value pairs (entries), where the keys have type K and the values have type V. There can be no two entries with the same key, and a key of reference type cannot be null. The interface describes these members in addition to ICollection<KeyValuePair<K,V>>:

+   - Read-only ICollection<K> returns a collection of the keys in the dictionary.
- Read-only ICollection<V> Returns a collection of values in the dictionary.
- Read-writerer[K k] gets or sets the value at dictionary key k. Throws ArgumentException when getting (but not setting) if k is not in the dictionary. Throws NotSupportedException if used to set an element in a read-only dictionary.
- void Add(K k, V v) inserts value v key k in the dictionary. Throws ArgumentException if k is already in the dictionary. Throws NotSupportedException if the dictionary is read-only.
- bool ContainsKey(K k) returns true if the dictionary contains an entry for key k; otherwise false.
- bool Remove(K k) removes the entry for key k, if any. Returns true if a key was removed.
- bool TryGetValue(K k, out V v) binds v to the value associated with key k and returns true if the dictionary contains an entry for k; otherwise binds v to default(V) and returns false.