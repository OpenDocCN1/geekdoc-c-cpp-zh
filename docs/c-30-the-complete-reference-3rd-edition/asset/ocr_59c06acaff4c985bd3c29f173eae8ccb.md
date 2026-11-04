```
if(fs.Error)
    Console.WriteLine("Error with index " + i);
}
}
```

This version of FailSoftArray works the same as the previous version, but it does not contain the explicitly declared backing fields.

Here are some restrictions that can apply to using access modifiers with accessors. First, only the set or get accessor can be modified, not both. Furthermore, the access modifier must be more restrictive than the access level of the property or indexer. Finally, an access modifier cannot be used when declaring an accessor within an interface or when implementing an accessor specified by an interface. (Interfaces are described in Chapter 12.)

# Using Indexers and Properties

Although the preceding examples have demonstrated the basic mechanism of indexers and properties, they haven't displayed their full power. To conclude this chapter, a class called RangeArray is developed that uses indexers and properties to create an array type in which the index range of the array is determined by the programmer.

As you know, in C# all arrays begin indexing at zero. However, some applications would benefit from an array that allows indexes to begin at any arbitrary point. For example, in some situations it might be more convenient for an array to begin indexing with 1. In another situation, it might be beneficial to allow negative indexes, such as an array that runs from -5 to 5. The RangeArray class developed here allows these and other types of indexing.

Using RangeArray, you can write code like this:

```
RangeArray ra = new RangeArray(-5, 10); // array with indexes from -5 to 10
for(int i=-5; i <= 10; i++) ra[i] = i; // index from -5 to 10
```

As you can guess, the first line constructs a RangeArray that runs from -5 to 10, inclusive. The first argument specifies the beginning index. The second argument specifies the ending index. Once ra has been constructed, it can be indexed from -5 to 10.

The entire RangeArray class is shown here, along with RangeArrayDemo, which demonstrates the array. As implemented here, RangeArray supports arrays of int, but you can change the data type, if desired.

```
/* Create a specifiable range array class.
   The RangeArray class allows indexing to begin at
   some value other than 0. When you create a RangeArray,
   you specify the beginning and ending index. Negative
   indexes are also allowed. For example, you can create
   arrays that index from -5 to 5, 1 to 10, or 50 to 56.
*/

using System;
class RangeArray {
    // Private data.
    int[] a; // reference to underlying array
```