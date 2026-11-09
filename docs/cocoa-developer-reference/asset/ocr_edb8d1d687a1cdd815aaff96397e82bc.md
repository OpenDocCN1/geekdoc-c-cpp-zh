# Figure 12.3

Inserting an object into a mutable array automatically adjusts the existing indexes.

![](bbox=[0.185, 0.191, 0.613, 0.436])

Related methods are available for removing, replacing, and exchanging objects. You can use `removeAllObjects` to empty the array.

You can hint a capacity for `NSMutableArray` by creating it with

```
aMutableArray = [NSMutableArray arrayWithCapacity: integer];
```

Mutable arrays expand and contract as needed. Hinting a capacity preassigns a block of memory, slightly increasing performance.

The capacity does not set the array bounds as it would for a C array. The bounds limit is set by the current item count, not the capacity.

The array contents must be a contiguous list. Gaps aren’t permitted. Attempting to insert an item at index: 50 in an empty array raises an exception, even when the capacity is 50.

If you need to implement a non-contiguous array, use `NSDictionary`, pairing objects with arbitrary index keys.

# Searching NSArray and NSMutableArray

`NSArray` and `NSMutableArray` organize data with the usual index model. `index:0` holds the first object, `index:1` the next, and so on. But these classes also implement powerful search options that allow random access.