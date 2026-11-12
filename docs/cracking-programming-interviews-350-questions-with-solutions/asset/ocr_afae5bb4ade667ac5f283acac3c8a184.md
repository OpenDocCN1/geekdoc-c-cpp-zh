+   - USE(q): Return the slot t ∈ S containing virtual page q ∈ P, or else NIL if q does not reside in primary memory.
+   - DROP(): Remove the least-recently used page q ∈ P from its slot t ∈ S, and return the non-empty slot t.

Describe briefly why these operations suffice to implement the LRU page replacement policy. Give an efficient implementation of this dynamic set.

# ## Solution

This problem had a very simple Θ(1) time implementation without making any simplifying assumptions. It should be assumed that for a paging system on any real computer, anything less than a Θ(1) time for any of those operations would simply be unacceptable.

We implement LRU by the use of

+   - A doubly linked list, call it L.
+   - A hash table, call it H.

The two data structures contain a structure holding the virtual page number q ∈ P and the corresponding physical page slot it occupies t ∈ S for all pages that are currently occupying physical memory slots. The hash table entries also hold a pointer to the linked list node corresponding to the virtual page q. The space requirement for this is therefore O(s).

In order to implement LRU, we need a complete ordering in terms of last access for every page currently occupying a physical memory slot. It is obvious to see that a doubly-linked list coupled with a move to front heuristic provides exactly this. Doubly-linked lists are convenient as cutting and pasting an element can be done in Θ(1) time, if we already have pointers to the element to cut and the element before or after where we will paste. Thus in order to support the DROP and USE operations in constant time, we use such a list, and arbitrarily define ordering to be from most recently used page at the head to least recently used at the tail. We thus also need to keep track of the head and tail of the doubly linked list so as to know where to cut and paste.

However, apart from the LRU information, we need the ability to lookup a certain virtual page and quickly extract the physical page slot it occupies. The INSERT procedure inserts this mapping into the data structure, whereas the USE procedure returns the mapping. This is an instance of the dictionary problem, which we know how to efficiently solve using a hash table. We use a chained hash table. The average access time in the table is Θ(1 + α), where α is the load factor defined as n/m where n is the number of things to store and m is the number of