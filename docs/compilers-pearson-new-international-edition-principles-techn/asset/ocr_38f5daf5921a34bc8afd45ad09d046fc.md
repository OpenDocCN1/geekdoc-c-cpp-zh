# 7.6. INTRODUCTION TO TRACE-BASED COLLECTION

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

# Algorithm 7.16: Cheney’s copying collector.

**INPUT:** A root set of objects, and a heap consisting of the *From* semispace, containing allocated objects, and the *To* semispace, all of which is free.