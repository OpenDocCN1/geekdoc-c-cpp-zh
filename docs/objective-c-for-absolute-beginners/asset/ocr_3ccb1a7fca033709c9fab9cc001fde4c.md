# 170 CHAPTER 8: Programming Basics in Objective-C

```
14 NSLog("%@", val);
15 }
```

In Listing 8–9 a new array is created similarly to the NSMutableSet. However, on line #11 new element is being inserted into the array at position 1. Remember, position 0 is the first element of the array. The contents of the array after the insert would look like:

| Index | Value |
|---|---|
| 0 | One |
| 1 | One and a Half |
| 2 | Two |
| 3 | Three |

Line #1 inserted a new element–the remaining elements were moved up in the array to make room. This is critical to know, especially if there is a code assumption that a particular index into an array will have a specific value.

With the NSMutableArrayArray, there are several ways to remove an object. Following are a few of the more commonly used methods:

+   * removeAllObjects – This method does as advertised. It removes all objects from a given NSMutableArray.
* removeLastObject – This method removes the last object at the end of the array. The array size is reduced by one.
* removeObjectAtIndex(NSInteger index) – This methods removes an object at a given index. The value is from 0 to length of the array–1.

# NSMutableDictionary

By this point, it may be pretty to you how the mutable versions of the collection classes–the NSMutableDictionary is no different. The NSMutableDictionary provides all the capabilities of NSDictionary but, of course, elements can be added and removed, as shown in Listing 8-10.

Listing 8–10. Adding objects to an NSMutableDictionary.

```
NSMutableDictionary *myDict = [NSMutableDictionary alloc];
[myDict setObject:"One" forKey:@"1"];
[myDict setObject:"Two" forKey:@"2"];
[myDict setObject:"Number Three" forKey:@"3"];
for (id val in mydict) {
NSLog("%@", val);
```