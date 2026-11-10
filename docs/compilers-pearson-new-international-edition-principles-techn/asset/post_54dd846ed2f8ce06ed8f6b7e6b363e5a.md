
contains bits telling which of the four states it is in. Initially, *Free* is the free list maintained by the memory manager, and all allocated objects are on the *Unreached* list (also maintained by the memory manager as it allocates chunks to objects).

```
1. Scanned = Unscanned = ∅;
2. move objects referenced by the root set from Unreached to Unscanned;
3. while (Unscanned ≠ ∅) {
4.     move object o from Unscanned to Scanned;
5.     for (each object o' referenced in o) {
6.         if (o' is in Unreached)
7.             move o' from Unreached to Unscanned;
8.     }
9. }
10. Free = Free ∪ Unreached;
11. Unreached = Scanned;
```

Figure 7.25: Baker’s mark-and-sweep algorithm

Lines (1) and (2) initialize *Scanned* to be the empty list, and *Unscanned* to have only the objects reached from the root set. Note that these objects were presumably on the list *Unreached* and must be removed from there. Lines (3) through (7) are a straightforward implementation of the basic marking algorithm, using these lists. That is, the for-loop of lines (5) through (7) examines the references in one unscanned object `o`, and if any of those references `o'` have not yet been reached, line (7) changes `o'` to the *Unscanned* state.

At the end, line (10) takes those objects that are still on the *Unreached* list and deallocates their chunks, by moving them to the *Free* list. Then, line (11) takes all the objects in state *Scanned*, which are the reachable objects, and reinitializes the *Unreached* list to be exactly those objects. Presumably, as the memory manager creates new objects, those too will be added to the *Unreached* list and removed from the *Free* list.

In both algorithms of this section, we have assumed that chunks returned to the free list remain as they were before deallocation. However, as discussed in Section 7.4.4, it is often advantageous to combine adjacent free chunks into larger chunks. If we wish to do so, then every time we return a chunk to the free list, either at line (10) of Fig. 7.21 or line (10) of Fig. 7.25, we examine the chunks to its left and right, and merge if one is free.

## 7.6.4 Mark-and-Compact Garbage Collectors

*Relocating* collectors move reachable objects around in the heap to eliminate memory fragmentation. It is common that the space occupied by reachable objects is much smaller than the freed space. Thus, after identifying all the holes, instead of freeing them individually, one attractive alternative is to relocate all the reachable objects into one end of the heap, leaving the entire rest of the heap as one free chunk. After all, the garbage collector has already analyzed every reference within the reachable objects, so updating them to point to the new locations does not require much more work. Thus, the references in the root set are all the references we need to change.

Having all the reachable objects in contiguous locations reduces fragmentation of the memory space, making it easier to house large objects. Also, by making the data occupy fewer cache lines and pages, relocation improves a program’s temporal and spatial locality, since new objects created at about the same time are allocated nearby chunks. Objects in nearby chunks can benefit from prefetching if they are used together. Further, the data structure for maintaining free space is simplified; instead of a free list, all we need is a pointer *free* to the beginning of the one free block.

Relocating collectors vary in whether they relocate in place or reserve space ahead of time for the relocation:

- A *mark-and-compact collector*, described in this section, compacts objects in place. Relocating in place reduces memory usage.
- The more efficient and popular *copying collector* in Section 7.6.5 moves objects from one region of memory to another. Reserving extra space for relocation allows reachable objects to be moved as they are discovered.

The mark-and-compact collector in Algorithm 7.15 has three phases:

- 1. First is a marking phase, similar to that of the mark-and-sweep algorithms described previously.
- 2. Second, the algorithm scans the allocated section of the heap and computes a new address for each of the reachable objects. New addresses are assigned from the low end of the heap, so there are no holes between reachable objects. The new address for each object is recorded in a structure called *NewLocation*.
- 3. Finally, the algorithm copies objects to their new locations, updating all references in the objects to point to the corresponding new locations. The needed addresses are found in *NewLocation*.

### Algorithm 7.15: A mark-and-compact garbage collector.

**INPUT:** A root set of objects, a heap, and *free*, a pointer marking the start of free space.

**OUTPUT:** The new value of pointer *free*.

**METHOD:** The algorithm is in Fig. 7.26; it uses the following data structures:

- 1. An *Unscanned* list, as in Algorithm 7.12.
- 2. Reached bits in all objects, also as in Algorithm 7.12. To keep our description simple, we refer to objects as “reached” or “unreached,” when we mean that their reached-bit is 1 or 0, respectively. Initially, all objects are unreached.
- 3. The pointer *free*, which marks the beginning of unallocated space in the heap.
- 4. The table *NewLocation*. This structure could be a hash table, search tree, or another structure that implements the two operations:
  - (a) Set *NewLocation(o)* to a new address for object *o*.
  - (b) Given object *o*, get the value of *NewLocation(o)*.

We shall not concern ourselves with the exact structure used, although you may assume that *NewLocation* is a hash table, and therefore, the “set” and “get” operations are each performed in average constant time, independent of how many objects are in the heap.

The first, or marking, phase of lines (1) through (7) is essentially the same as the first phase of Algorithm 7.12. The second phase, lines (8) through (12), visits each chunk in the allocated part of the heap, from the left, or low end. As a result, chunks are assigned new addresses that increase in the same order as their old addresses. This ordering is important, since when we relocate objects, we can do so in a way that assures we only move objects left, into space that was formerly occupied by objects we have moved already.

Line (8) starts the *free* pointer at the low end of the heap. In this phase, we use *free* to indicate the first available new address. We create a new address only for those objects *o* that are marked as reached. Object *o* is given the next available address at line (10), and at line (11) we increment *free* by the amount of storage that object *o* requires, so *free* again points to the beginning of free space.

In the final phase, lines (13) through (17), we again visit the reached objects, in the same from-the-left order as in the second phase. Lines (15) and (16) replace all internal pointers of a reached object *o* by their proper new values, using the *NewLocation* table to determine the replacement. Then, line (17) moves the object *o*, with the revised internal references, to its new location. Finally, lines (18) and (19) retarget pointers in the elements of the root set that are not themselves heap objects, e.g., statically allocated or stack-allocated objects. Figure 7.27 suggests how the reachable objects (those that are not shaded) are moved down the heap, while the internal pointers are changed to point to the new locations of the reached objects. □

## 7.6.5 Copying collectors

A copying collector reserves, ahead of time, space to which the objects can move, thus breaking the dependency between tracing and finding free space.

```
/* mark */
1)  Unscanned = set of objects referenced by the root set;
2)  while (Unscanned ≠ ∅) {
3)      remove object o from Unscanned;
4)      for (each object o′ referenced in o) {
5)          if (o′ is unreached) {
6)              mark o′ as reached;
7)              put o′ on list Unscanned;
        }
    }
/* compute new locations */
8)  free = starting location of heap storage;
9)  for (each chunk of memory o in the heap, from the low end) {
10)     if (o is reached) {
11)         NewLocation(o) = free;
12)         free = free + sizeof(o);
        }
    }
/* retarget references and move reached objects */
13) for (each chunk of memory o in the heap, from the low end) {
14)     if (o is reached) {
15)         for (each reference o.r in o)
16)             o.r = NewLocation(o.r);
17)         copy o to NewLocation(o);
        }
    }
18) for (each reference r in the root set)
19)     r = NewLocation(r);
```

Figure 7.26: A Mark-and-Compact Collector

The memory space is partitioned into two semispaces, A and B. The mutator allocates memory in one semispace, say A, until it fills up, at which point the mutator is stopped and the garbage collector copies the reachable objects to the other space, say B. When garbage collection completes, the roles of the semispaces are reversed. The mutator is allowed to resume and allocate objects in space B, and the next round of garbage collection moves reachable objects to space A. The following algorithm is due to C. J. Cheney.

### Algorithm 7.16: Cheney’s copying collector.

**INPUT:** A root set of objects, and a heap consisting of the *From* semispace, containing allocated objects, and the *To* semispace, all of which is free.
