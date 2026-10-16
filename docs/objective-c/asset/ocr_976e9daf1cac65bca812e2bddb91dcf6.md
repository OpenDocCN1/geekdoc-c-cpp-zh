```
[result addObject:transformObj(obj)];
}
```

```
[array enumerateObjectsUsingBlock:theBlock];
```

When this completes, the result array should contain all the elements of the original array but with whatever transformation the transformObj function is doing.

To do the same, but only over a subset of the array, you can use the method -enumerateObjectsAtIndexes:withBlock:. You can also access a subset of the array by using the method -indexesOfObjectsPassingTest:. This convenient method allows you to pass a block to which each object will be given. If the block returns YES, then the object's index will be included in the returned array, otherwise it will not. This makes filtering a breeze with blocks.

Another method of performing a similar procedure might be to use the object methods -makeObjectsPerformSelector: or -makeObjectsPerformSelector:withObject:, which perform an enumeration of the elements of the array and call the given selector on each object. The disadvantage of this method as opposed to the ones that take blocks is that the selector has to be defined on the class of the objects in the array. This can be difficult in some cases, and might even force you to make a category to extend third-party classes for this purpose.

# Summary

Collection classes are a vital part of any standard library. Objective-C, fortunately, has an excellent group of collection classes that make working with groups of objects easy. With NSArray for ordered collections, NSDictionary for associative collections, and NSSet for unordered collections, you have all the tools you need.