+   2. Reached bits in all objects, also as in Algorithm 7.12. To keep our description simple, we refer to objects as “reached” or “unreached,” when we mean that their reached-bit is 1 or 0, respectively. Initially, all objects are unreached.
+   3. The pointer *free*, which marks the beginning of unallocated space in the heap.
+   4. The table *NewLocation*. This structure could be a hash table, search tree, or another structure that implements the two operations:
+       (a) Set *NewLocation*(o) to a new address for object *o*.
+       (b) Given object *o*, get the value of *NewLocation*(o).

We shall not concern ourselves with the exact structure used, although you may assume that *NewLocation* is a hash table, and therefore, the “set” and “get” operations are each performed in average constant time, independent of how many objects are in the heap.

The first, or marking, phase of lines (1) through (7) is essentially the same as the first phase of Algorithm 7.12. The second phase, lines (8) through (12), visits each chunk in the allocated part of the heap, from the left, or low end. As a result, chunks are assigned new addresses that increase in the same order as their old addresses. This ordering is important, since when we relocate objects, we can do so in a way that assures we only move objects left, into space that was formerly occupied by objects we have moved already.

Line (8) starts the *free* pointer at the low end of the heap. In this phase, we use *free* to indicate the first available new address. We create a new address only for those objects *o* that are marked as reached. Object *o* is given the next available address at line (10), and at line (11) we increment *free* by the amount of storage that object *o* requires, so *free* again points to the beginning of free space.

In the final phase, lines (13) through (17), we again visit the reached objects, in the same from-the-left order as in the second phase. Lines (15) and (16) replace all internal pointers of a reached object *o* by their proper new values, using the *NewLocation* table to determine the replacement. Then, line (17) moves the object *o*, with the revised internal references, to its new location. Finally, lines (18) and (19) retarget pointers in the elements of the root set that are not themselves heap objects, e.g., statically allocated or stack-allocated objects. Figure 7.27 suggests how the reachable objects (those that are not shaded) are moved down the heap, while the internal pointers are changed to point to the new locations of the reached objects. □

# ### 7.6.5 Copying collectors

A copying collector reserves, ahead of time, space to which the objects can move, thus breaking the dependency between tracing and finding free space.