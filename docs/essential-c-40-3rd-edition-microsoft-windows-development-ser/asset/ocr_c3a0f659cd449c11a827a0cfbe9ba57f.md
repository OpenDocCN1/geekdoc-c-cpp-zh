variable. In this example, the key data type used is Guid, and the value data type is string.

The second thing to notice in Listing 16.6 is the reuse of the same index. In the first assignment, no dictionary element corresponds to key. Instead of throwing an out-of-bounds exception, as an array would, dictionary collection classes insert a new object. During the second assignment, an element with the specified key already exists, so instead of inserting an additional element, the existing element corresponding to key is updated from "object" to "byte".

Accessing a value from a dictionary using the index operator ([]) with a nonexistent key throws an exception of type System.Collections.Generic.KeyNotFoundException. The ContainsKey() method, however, allows you to check whether a particular key is used before accessing its value, thereby avoiding the exception. Also, since the keys are stored in a hash table, the search is relatively efficient.

By contrast, checking whether there is a particular value in the dictionary contrasts is a time-consuming operation with linear performance characteristics. To do this you use the ContainsValue() method, which searches sequentially through each element in the collection.

You remove a dictionary element using the Remove() method, passing the key, not the element value.

There is no particular order for the dictionary classes. Elements are arranged into a hash table using hash codes for rapid retrieval (acquired by calling GetHashCode() on the key). Iterating through a dictionary class using the foreach loop, therefore, accesses values in no particular order. Because both the key and the element value are required to add an element to the dictionary, the data type returned from the foreach loop is KeyValuePair<TKey, TValue> for Dictionary<TKey, TValue>. Listing 16.7 shows a snippet of code demonstrating the foreach loop with the Dictionary<TKey, TValue> collection class. The output appears in Output 16.3.

# LISTING 16.7: Iterating over Dictionary<TKey, TValue> with foreach

```
using System;
using System.Collections.Generic;

class Program
{
   static void Main()
```