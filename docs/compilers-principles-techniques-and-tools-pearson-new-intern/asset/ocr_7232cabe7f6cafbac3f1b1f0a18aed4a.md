contains bits telling which of the four states it is in. Initially, _Free_ is the free list maintained by the memory manager, and all allocated objects are on the _Unreached_ list (also maintained by the memory manager as it allocates chunks to objects).

```
1)  `Scanned = Unscanned = ∅;`
2)  move objects referenced by the root set from `Unreached` to `Unscanned`;
3)  `while (Unscanned ≠ ∅) {`
4)      move object o from `Unscanned` to `Scanned`;
5)      `for` (each object o′ referenced in o) {
6)          `if` (o′ is in `Unreached`)
7)              move o′ from `Unreached` to `Unscanned`;
        }
    }
8)  `Free = Free ∪ Unreached;`
9)  `Unreached = Scanned;`
```

Figure 7.25: Baker’s mark-and-sweep algorithm

Lines (1) and (2) initialize _Scanned_ to be the empty list, and _Unscanned_ to have only the objects reached from the root set. Note that these objects were presumably on the list _Unreached_ and must be removed from there. Lines (3) through (7) are a straightforward implementation of the basic marking algorithm, using these lists. That is, the for-loop of lines (5) through (7) examines the references in one unscanned object o, and if any of those references o′ have not yet been reached, line (7) changes o′ to the _Unscanned_ state.

At the end, line (8) takes those objects that are still on the _Unreached_ list and deallocates their chunks, by moving them to the _Free_ list. Then, line (9) takes all the objects in state _Scanned_, which are the reachable objects, and reinitializes the _Unreached_ list to be exactly those objects. Presumably, as the memory manager creates new objects, those too will be added to the _Unreached_ list and removed from the _Free_ list. □

In both algorithms of this section, we have assumed that chunks returned to the free list remain as they were before deallocation. However, as discussed in Section 7.4.4, it is often advantageous to combine adjacent free chunks into larger chunks. If we wish to do so, then every time we return a chunk to the free list, either at line (10) of Fig. 7.21 or line (8) of Fig. 7.25, we examine the chunks to its left and right, and merge if one is free.

# 7.6.4  Mark-and-Compact Garbage Collectors

_Relocating_ collectors move reachable objects around in the heap to eliminate memory fragmentation. It is common that the space occupied by reachable objects is much smaller than the freed space. Thus, after identifying all the holes,