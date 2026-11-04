| Method | Description |
|---|---|
| public void Add(TK k, TV v) | Adds the key/value pair specified by k and v to the dictionary. If k is already in the dictionary, then its value is unchanged and an ArgumentException is thrown. |
| public bool ContainsKey(TK k) | Returns true if k is a key in the invoking dictionary. Returns false otherwise. |
| public bool ContainsValue(TV v) | Returns true if v is a value in the invoking dictionary. Returns false otherwise. |
| public SortedDictionary.Enumerator<TK, TV> GetEnumerator() | Returns an enumerator for the invoking dictionary. |
| public bool Remove(TK k) | Removes k from the dictionary. Returns true if successful. Returns false if k was not in the dictionary. |

TABLE 24-17 A Sampling of Methods Defined by SortedDictionary<TK, TV>

In addition to the properties defined by the interfaces that it implements, SortedDictionary<TK, TV> defines the following properties:

| Property | Description |
|---|---|
| public IComparer<TK> Comparer { get; } | Obtains the comparer for the invoking dictionary. |
| public SortedDictionary<TK, TV>.KeyCollection Keys { get; } | Obtains a collection of the keys. |
| public SortedDictionary<TK, TV>.ValueCollection Values { get; } | Obtains a collection of the values. |

Notice that the keys and values contained within the collection are available as separate lists through the Keys and Values properties. The types

SortedDictionary<TK, TV>.KeyCollection
SortedDictionary<TK, TV>.ValueCollection

are collections that implement both the generic and non-generic forms of ICollection and IEnumerable.

SortedDictionary<TK, TV> defines the following indexer (which is specified by IDictionary<TK, TV>):

public TV this[TK key] { get; set; }

You can use this indexer to get or set the value of an element. You can also use it to add a new element to the collection. Notice that the "index" is not actually an index, but rather the key of the item.