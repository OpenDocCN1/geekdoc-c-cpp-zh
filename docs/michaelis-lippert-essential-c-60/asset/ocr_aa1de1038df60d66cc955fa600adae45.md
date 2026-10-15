Thus, when selecting a collection class to solve some data storage or retrieval problem, the first two interfaces to look for are IList<T> and IDictionary<TKey, TValue>. These interfaces indicate whether the collection type is focused on retrieval of a value when given its positional index or retrieval of a value when given its associated key.

Both of these interfaces require that a class that implements them provide an indexer. In the case of IList<T>, the operand of the indexer corresponds to the position of the element being retrieved: The indexer takes an integer and gives you access to the nth element in the list. In the case of the IDictionary<TKey, TValue> interface, the operand of the indexer corresponds to the key associated with a value, and gives you access to that value.

# ICollection<T>

Both IList<T> and IDictionary<TKey, TValue> implement ICollection<T>. A collection that does not implement either IList<T> or IDictionary<TKey, TValue> will more than likely implement ICollection<T> (although not necessarily, because collections could implement the lesser requirement of IEnumerable or IEnumerable<T>). ICollection<T> is derived from IEnumerable<T> and includes two members: Count and CopyTo().

+   - The Count property returns the total number of elements in the collection. Initially, it might appear that this would be sufficient to iterate through each element in the collection using a for loop, but, in fact, the collection would also need to support retrieval by index, which the ICollection<T> interface does not include (although IList<T> does include it).

+   - The CopyTo() method provides the ability to convert the collection into an array. This method includes an index parameter so that you can specify where to insert elements in the target array. To use the method, you must initialize the array target with sufficient capacity, starting at the index, to contain all the elements in ICollection<T>.

# Primary Collection Classes

Five key categories of collection classes exist, and they differ from one another in terms of how data is inserted, stored, and retrieved. Each generic class is located in the System.Collections.Generic namespace, and their nongeneric equivalents are found in the System.Collections namespace.