# Chapter 8 = Hash Tables

The following section discusses another important problem with open addressing.

# Removing Items

Although open addressing lets you to add and find items reasonably quickly, at least if the array isn't too full, it doesn't allow you to remove items the way chaining does. An item in the array might be part of another item's probe sequence. If you remove an item, you may break the other item's probe sequence, so you can no longer find the second value.

For example, suppose items A and B map to the same index $I_x$. Item A is added first at index $I_x$, so when you add item B, it goes to the second position in its probe sequence, $I_f$.

Now suppose you remove item A. If you try to find item B, you initially look at index $I_x$. Because that is now empty, you incorrectly conclude that item B isn't present.

One solution to this problem is to mark the entry as deleted instead of resetting the array to the empty value. For example, if the array holds 32-bit integers, you might use the value -2,147,483,648 to mean that an entry has no value and -2,147,483,648 to mean that the value has been deleted.

When you search for a value, continue searching if you find the deleted value. When you insert a new value into the hash table, you can place it in a previously deleted entry if you find one in the probe sequence.

One drawback of this approach is that if you add and then remove items, the table may become full of deleted entries. That won't slow down insertions. In the worst case, if the array is completely full of current and deleted items, you might have to search the entire array to find an item or to conclude that it isn't present.

If you delete many items, you can refresh the current values and reset the deleted array locations so that they hold the empty value. If the array contains N items and has a reasonable fill percentage, this should take only O(N) time.

# Linear Probing

In linear probing, the collision-resolution policy adds a constant number, called the *stride* and usually set to 1, to each location to generate a probe sequence. Each time the algorithm adds 1, it takes the result modulus the size of the array, so the sequence wraps around to the beginning of the array if necessary.