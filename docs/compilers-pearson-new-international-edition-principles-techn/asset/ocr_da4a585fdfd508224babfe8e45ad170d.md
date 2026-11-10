# 7.6. INTRODUCTION TO TRACE-BASED COLLECTION

```
```text
1)  CopyingCollector() {
        for (all objects o in From space) NewLocation(o) = NULL;
        unscanned = free = starting address of To space;
        for (each reference r in the root set)
            replace r with LookupNewLocation(r);
        while (unscanned ≠ free) {
            o = object at location unscanned;
            for (each reference o.r within o)
                o.r = LookupNewLocation(o.r);
            unscanned = unscanned + sizeof(o);
        }
    }

    /* Look up the new location for object if it has been moved. */
    /* Place object in Unscanned state otherwise. */
11) LookupNewLocation(o) {
12)     if (NewLocation(o) = NULL) {
13)         NewLocation(o) = free;
14)         free = free + sizeof(o);
15)         copy o to NewLocation(o);
        }
16)     return NewLocation(o);
    }
```
```

Figure 7.28: A Copying Garbage Collector

state. Thus, free always leads unscanned, and when the latter catches up to the former, there are no more Unscanned objects, and we are done with the garbage collection. Notice that we do our work within the To space, although all references within objects examined at line (8) lead us back to the From space.

Lines (4) and (5) handle the objects reached from the root set. Note that as a side effect, some of the calls to LookupNewLocation at line (5) will increase free, as chunks for these objects are allocated within To. Thus, the loop of lines (6) through (10) will be entered the first time it is reached, unless there are no objects referenced by the root set (in which case the entire heap is garbage). This loop then scans each of the objects that has been added to To and is in the Unscanned state. Line (7) takes the next unscanned object, o. Then, at lines (8) and (9), each reference within o is translated from its value in the From semispace to its value in the To semispace. Notice that, as a side effect, if a reference within o is to an object we have not reached previously, then the call to LookupNewLocation at line (9) creates space for that object in the To space and moves the object there. Finally, line (10) increments unscanned to point to the next object, just beyond o in the To space. □