# Selecting an Implementation

If n items are in a linked chain, can you possibly traverse the middle one? From its beginning until you have visited n /2 items. But, as you will see in the answer to the question posed before, just this step will take longer than the entire binary search of an array. Furthermore, you would have the same problem of finding the "middle" at each recursive step. It is thus impractical to perform a binary search for the link-based implementation. Observation is extremely significant.

A binary search is impractical with a link-based implementation

On the other hand, if n items are in an array, the item is at location n /2 and can be accessed directly. Thus, a binary search of an array considers less time than an algorithm that must inspect every item in the dictionary. What does "considerably less time" mean? As you know, without the ability to perform a binary search, you must inspect every item in the dictionary, either to locate an item with a particular key or to detect that such an item is not present. In other words, if a dictionary has size n, you will have to inspect as many as n items; thus search is O(n). How well can you do with a binary search? Recall that that a binary search is O(log n) in its worst case and an O(log n) algorithm is significantly more efficient than an O(n) algorithm. For example, log,1024=10 and log,1048=20. For a large dictionary, the binary search has no enormous advantage.

If you know the dictionary's maximum size, a sorted-array implementation is appropriate for frequent retrievals

Because this is large, you must choose an implementation for which a binary search is practical. As you have just seen, observation eliminates the link-based implementation. The array-based implementation is here, because you know the size of the thousands.

If you do not know the dictionary's maximum size, use a binary search tree in the implementation

An implementation using a binary search tree is also a good choice for retrieval-oriented applications. As you see in chapter 15, searching a binary search tree is O(log n) if the tree is balanced. Because the insertion creates a balanced tree that remains balanced and is assured of an efficient search. Points in a binary search tree space as scenario A, this cost is relatively insignificant when the data items are large.

Scenario C: Insertion, removal, and traversal in sorted order. If your local library has computerized its catalog of books, you perform a removal operation when you access this catalog. The library uses insertion and removal operations to update the catalog and a traversal to save the entire entry in a file. Presumably, the removal is the most frequent operation, but the other operations are not infrequent enough to ignore. If so, this scenario would be the same as scenario B!

To insert an item whose key is X, you must first determine the item in the dictionary's sorted order. Similarly, to the removal of an item that has X as its key, you must first find its location. Thus, both add and remove operations perform the following steps:

+   1. Find the appropriate position in the dictionary.
2. Insert into (or remove) this position.

Both add and remove perform these two steps

Step 1 is far more efficient if the dictionary implementation is array instead of linked. For an array-based implementation, where the new item X belongs—in the case of insertion—where the item is located. For a link-based implementation, you know from the discussion in scenario B that a binary search is impractical, and so you must traverse the chain from beginning. It takes significantly less time than it does to traverse a linked chain.

Use an array-based implementation for step 1

Step 2 is, however, the array-based implementation is superior with respect to step 1 of add and remove. However, as you have guessed, the link-based implementation is better for step 2, the actual insertion or removal of the item. Under the array-based implementation, add must shift entries to make room for the new item, as Figure 18-7a illustrates. The worst case would require that every array be shifted. On the other hand, the link-based

Use a link-based implementation for step 2