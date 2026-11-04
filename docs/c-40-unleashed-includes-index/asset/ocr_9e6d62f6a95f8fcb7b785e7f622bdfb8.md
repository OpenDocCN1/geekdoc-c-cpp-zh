# # ArrayList

An ArrayList provides array-like access, using indexers, while having the capability to grow dynamically as needed. The collection maintains the order in which items were added and provides the ability to insert and remove items. The following are typical operations:

```
```csharp
var lst = new ArrayList();
lst.Add(1);                          // {  1 }
lst.AddRange(new[] { 2, 3, 7, 6, 5, 4 }); // {  1, 2, 3, 7, 6, 5, 4 }
lst.Insert(index: 0, value: 0);          // {  0, 1, 2, 3, 7, 6, 5, 4 }
lst.RemoveAt(index: 4);                  // {  0, 1, 2, 3,    6, 5, 4 }
lst.Remove(ob: 1);                       // {  0,    2, 3,    6, 5, 4 }
lst.RemoveRange(index: 2, count: 3);     // {  0,    2,          4 }
lst.Reverse();                           // {  4, 2, 0 }
lst.Sort();                              // {  0, 2, 4 }
bool hasTwo = lst.Contains(2);           // true
int two = (int)lst[1];                   // 2
```
```

From a performance point of view, Add is a constant time operation unless the list's capacity is reached, at which point a new storage array needs to be allocated, copying the original array's elements over. If you know upfront what the capacity of the list is going to be, use the constructor overload that allows specifying an initial capacity.

Because the internal storage is a plain array, lookup operations like Contains require sequential scanning of the list (but also when an element needs to be found for removal), which will pose a problem for larger collections.

Operations such as Insert and index-based Remove are linear in the size of the list as well because elements have to be moved around in the array, shifting elements either to the right for an Insert or to the left for a Remove.

# ## BIG O

MSDN documentation for collections provides a Big O cost for every method. The Big O notation is used in complexity theory to indicate an upper bound on the computational resources required to execute the underlying algorithm. O(1) means constant time, O(n) means linear in the size of the collection, and similar notations are used for quadratic or logarithmic complexity in terms of the size of the collection. Obviously, constant time is the best, followed by logarithmic time. When things get linear or quadratic, you might be in for a problem if the collection size is getting high.

Let desired characteristics be your first guide when deciding what collection type to use. If you need things to have a linear ordering, use some kind of list; if you need fast lookups, a hash table is better; avoiding duplicates can be done using a set; and so on. After you've determined your needs and candidates for the collection types that have those characteristics, get some idea about the costs of the various operations.