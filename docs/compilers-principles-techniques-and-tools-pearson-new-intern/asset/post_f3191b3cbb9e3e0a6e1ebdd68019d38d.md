
```text
/* mark */
1) Unscanned = set of objects referenced by the root set;
2) while (Unscanned ≠ ∅) {
3)     remove object o from Unscanned;
4)     for (each object o' referenced in o) {
5)         if (o' is unreached) {
6)             mark o' as reached;
7)             put o' on list Unscanned;
        }
    }
}
/* compute new locations */
8) free = starting location of heap storage;
9) for (each chunk of memory o in the heap, from the low end) {
10)    if (o is reached) {
11)        NewLocation(o) = free;
12)        free = free + sizeof(o);
    }
}
/* retarget references and move reached objects */
13) for (each chunk of memory o in the heap, from the low end) {
14)    if (o is reached) {
15)        for (each reference o.r in o)
16)            o.r = NewLocation(o.r);
17)        copy o to NewLocation(o);
    }
}
18) for (each reference r in the root set)
19)     r = NewLocation(r);
```

Figure 7.26: A Mark-and-Compact Collector

The memory space is partitioned into two *semispaces*, A and B. The mutator allocates memory in one semispace, say A, until it fills up, at which point the mutator is stopped and the garbage collector copies the reachable objects to the other space, say B. When garbage collection completes, the roles of the semispaces are reversed. The mutator is allowed to resume and allocate objects in space B, and the next round of garbage collection moves reachable objects to space A. The following algorithm is due to C. J. Cheney.

**Algorithm 7.16:** Cheney’s copying collector.

**INPUT:** A root set of objects, and a heap consisting of the *From* semispace, containing allocated objects, and the *To* semispace, all of which is free.

![](img/a29d16e454785bb105e96ef448ac07f6_484_0.png)

Figure 7.27: Moving reached objects to the front of the heap, while preserving internal pointers

**OUTPUT:** At the end, the *To* semispace holds the allocated objects. A *free* pointer indicates the start of free space remaining in the *To* semispace. The *From* semispace is completely free.

**METHOD:** The algorithm is shown in Fig. 7.28. Cheney’s algorithm finds reachable objects in the *From* semispace and copies them, as soon as they are reached, to the *To* semispace. This placement groups related objects together and may improve spatial locality.

Before examining the algorithm itself, which is the function *CopyingCollector* in Fig. 7.28, consider the auxiliary function *LookupNewLocation* in lines (11) through (16). This function takes an object *o* and finds a new location for it in the *To* space if *o* has no location there yet. All new locations are recorded in a structure *NewLocation*, and a value of NULL indicates *o* has no assigned location.⁴ As in Algorithm 7.15, the exact form of structure *NewLocation* may vary, but it is fine to assume that it is a hash table.

⁴ In a typical data structure, such as a hash table, if *o* is not assigned a location, then there simply would be no mention of it in the structure.

If we find at line (12) that *o* has no location, then it is assigned the beginning of the free space within the *To* semispace, at line (13). Line (14) increments the *free* pointer by the amount of space taken by *o*, and at line (15) we copy *o* from the *From* space to the *To* space. Thus, the movement of objects from one semispace to the other occurs as a side effect, the first time we look up the new location for the object. Regardless of whether the location of *o* was or was not previously established, line (16) returns the location of *o* in the *To* space.

Now, we can consider the algorithm itself. Line (2) establishes that none of the objects in the *From* space have new addresses yet. At line (3), we initialize two pointers, *unscanned* and *free*, to the beginning of the *To* semispace. Pointer *free* will always indicate the beginning of free space within the *To* space. As we add objects to the *To* space, those with addresses below *unscanned* will be in the *Scanned* state, while those between *unscanned* and *free* are in the *Unscanned* state. Thus, free always leads unscanned, and when the latter catches up to the former, there are no more Unscanned objects, and we are done with the garbage collection. Notice that we do our work within the To space, although all references within objects examined at line (8) lead us back to the From space.

```text
1)  CopyingCollector () {
2)      for (all objects o in From space) NewLocation(o) = NULL;
3)      unscanned = free = starting address of To space;
4)      for (each reference r in the root set)
5)          replace r with LookupNewLocation(r);
6)      while (unscanned ≠ free) {
7)          o = object at location unscanned;
8)          for (each reference o.r within o)
9)              o.r = LookupNewLocation(o.r);
10)         unscanned = unscanned + sizeof(o);
        }
    }

    /* Look up the new location for object if it has been moved. */
    /* Place object in Unscanned state otherwise. */
11) LookupNewLocation(o) {
12)     if (NewLocation(o) == NULL) {
13)         NewLocation(o) = free;
14)         free = free + sizeof(o);
15)         copy o to NewLocation(o);
        }
16)     return NewLocation(o);
    }
```

Figure 7.28: A Copying Garbage Collector

Lines (4) and (5) handle the objects reached from the root set. Note that as a side effect, some of the calls to LookupNewLocation at line (5) will increase free, as chunks for these objects are allocated within To. Thus, the loop of lines (6) through (10) will be entered the first time it is reached, unless there are no objects referenced by the root set (in which case the entire heap is garbage). This loop then scans each of the objects that has been added to To and is in the Unscanned state. Line (7) takes the next unscanned object, o. Then, at lines (8) and (9), each reference within o is translated from its value in the From semispace to its value in the To semispace. Notice that, as a side effect, if a reference within o is to an object we have not reached previously, then the call to LookupNewLocation at line (9) creates space for that object in the To space and moves the object there. Finally, line (10) increments unscanned to point to the next object, just beyond o in the To space. □

**Exercise 7.6.4:** Suppose we execute Cheney’s copying garbage collection algorithm on each of the networks of Exercise 7.6.1. Also, suppose that

- i. Each object has size 100 bytes,
- ii. The unscanned list is managed as a queue, and when an object has more than one pointer, the reached objects are added to the queue in alphabetical order, and
- iii. The *From* semispace starts at location 0, and the *To* semispace starts at location 10,000.

What is the value of *NewLocation(o)* for each object *o* that remains after garbage collection?

## 7.7 Short-Pause Garbage Collection

Simple trace-based collectors do stop-the-world-style garbage collection, which may introduce long pauses into the execution of user programs. We can reduce the length of the pauses by performing garbage collection one part at a time. We can divide the work in time, by interleaving garbage collection with the mutation, or we can divide the work in space by collecting a subset of the garbage at a time. The former is known as *incremental collection* and the latter is known as *partial collection*.

An incremental collector breaks up the reachability analysis into smaller units, allowing the mutator to run between these execution units. The reachable set changes as the mutator executes, so incremental collection is complex. As we shall see in Section 7.7.1, finding a slightly conservative answer can make tracing more efficient.

The best known of partial-collection algorithms is *generational garbage collection*; it partitions objects according to how long they have been allocated and collects the newly created objects more often because they tend to have a shorter lifetime. An alternative algorithm, the *train algorithm*, also collects a subset of garbage at a time, and is best applied to more mature objects. These two algorithms can be used together to create a partial collector that handles younger and older objects differently. We discuss the basic algorithm behind partial collection in Section 7.7.3, and then describe in more detail how the generational and train algorithms work.

Ideas from both incremental and partial collection can be adapted to create an algorithm that collects objects in parallel on a multiprocessor; see Section 7.8.1.

### 7.7.1 Incremental Garbage Collection

Incremental collectors are conservative. While a garbage collector must not collect objects that are not garbage, it does not have to collect all the garbage
