Following are descriptions of the interfaces contained within the System.Collections.Generic namespace.

| Interface | Description |
|---|---|
| `ICollection<(Of <(T)>)>` | Defines methods to manipulate generic collections |
| `IComparer<(Of <(T)>)>` | Defines a method that a type implements to compare two objects |
| `IDictionary<(Of <(TKey, TValue)>)>` | Represents a generic collection of key/value pairs |
| `IEnumerable<(Of <(T)>)>` | Exposes the enumerator, which supports a simple iteration over a collection of a specified type |
| `IEnumerator<(Of <(T)>)>` | Supports a simple iteration over a generic collection |
| `IEqualityComparer<(Of <(T)>)>` | Defines methods to support the comparison of objects for equality |
| `IList<(Of <(T)>)>` | Represents a collection of objects that can be individually accessed by index |

Prior to .NET 2.0, all the data structures contained in the System.Collection namespace are object-based. With .NET 2.0, Microsoft has released generic equivalents of some of these classes. The following table shows the mapping of these classes in the two namespaces.

| System.Collection | System.Collection.Generic |
|---|---|
| Comparer | Comparer<T> |
| HashTable | Dictionary<K, T> |
| - | LinkedList<T> |
| ArrayList | List<T> |
| Queue | Queue<T> |
| SortedList | SortedDictionary<K, T> |
| Stack | Stack<T> |
| ICollection | ICollection<T> |
| System.IComparable | IComparable<T> |
| IDictionary | IDictionary<K, T> |
| IEnumerable | IEnumerable<T> |
| IEnumerator | IEnumerator<T> |
| IList | IList<T> |