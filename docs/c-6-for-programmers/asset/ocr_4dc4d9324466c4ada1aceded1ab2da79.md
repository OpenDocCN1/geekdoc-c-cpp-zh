Figure 19.1 lists some of the collection interfaces in namespace `System.Collections.Generic`, which also have legacy object-based analogs in `System.Collections`. Many collection classes implement these interfaces. You may also provide implementations specific to your own requirements.

| Interface | Description |
|---|---|
| `IEnumerable<T>` | An object that can be enumerated—for example, a `foreach` loop can iterate over such an object’s elements. This interface contains one method, `GetEnumerator`, which returns an `IEnumerator<T>` object, which (as you’ll see in Section 19.3) can be used many to iterate through a collection. In fact, `foreach` uses a collection’s `IEnumerator<T>` object behind the scenes. `ICollection<T>` extends `IEnumerable<T>` so all collection classes implement `IEnumerable<T>` directly or indirectly. |
| `ICollection<T>` | The interface from which interfaces `IList<T>` and `IDictionary<K,V>` inherit. Contains a `Count` property to determine the size of a collection and a `CopyTo` method for copying a collection’s contents to a traditional array, and an `IsReadOnly` property. |
| `IList<T>` | An ordered collection that can be manipulated like an array. Provides a `[]` operator (known as an indexer) for accessing elements with an int index. Also has methods for searching and modifying a collection, including `Add`, `Remove`, `Contains` and `IndexOf`. |
| `IDictionary<K,V>` | A collection of values, indexed by an arbitrary “key” object of type K. Provides an indexer (`[]`) for accessing elements by key and methods for modifying the collection (e.g., `Add`, `Remove`). `IDictionary<K,V>` property `Keys` contains all the keys, and property `Values` contains all the stored values. |

**Fig. 19.1**  |  Some common generic collection interfaces.

# Namespace `System.Collections.Generic`

With the collections of the `System.Collections.Generic` namespace, you can specify the exact type that will be stored in a collection. This provides two key benefits over the object-based legacy collections:

+   - *Compile-time type checking* ensures that you’re using appropriate types with your collection and, if not, the compiler issues error messages.
+   - Any item you retrieve from a generic collection will have the correct type. With object-based collections, any item you retrieve is returned as an object. Then, you must *explicitly cast* the object to the type that your program manipulates. This could lead to `InvalidCastException`s at execution time if the referenced object does not have the appropriate type.