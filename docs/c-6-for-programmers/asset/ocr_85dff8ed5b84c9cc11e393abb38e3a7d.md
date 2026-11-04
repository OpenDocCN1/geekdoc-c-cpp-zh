statements. When Line 81 executes, however, Count and Capacity are both 4, so the List doubles its Capacity to 8 and the Count becomes 5, leaving room for three more elements.

# *Doubling the Capacity*

When a List grows, it must (behind the scenes) create a larger internal array and copy each element to the new array. This is a time-consuming operation. It would be inefficient for the List to grow each time an element is added. To minimize the number of memory reallocations, a List doubles its capacity when more memory is required.¹

> **Performance Tip 9.1**
> 
> *Doubling a List's capacity is an efficient way for a List to grow quickly to be "about the right size." This operation is much more efficient than growing a List by only as much space as it takes to hold the element(s) being added. A disadvantage is that the List might occupy more space than it requires. This is a classic example of the space/time trade-off.*

![](bbox=[0.161, 0.262, 0.211, 0.299])

> **Performance Tip 9.2**
> 
> *It can be wasteful to double a List's size when more space is needed. For example, a full List of 1,000,000 elements resizes to accommodate 2,000,000 elements when one new element is added. This leaves 999,999 unused elements. You can use TrimExcess (as in your List object) to reduce a List's capacity to its current Count. You also can set the Capacity directly to control space usage better—for example, if you know a List will never grow beyond 100 elements, you can preallocate that space by assigning 100 to the List's Capacity or using the List constructor that receives an initial capacity.*

![](bbox=[0.161, 0.369, 0.211, 0.405])

# 9.5 **Querying the Generic List Collection Using LINQ**

As with arrays, you can use LINQ to Objects to query Lists. In Fig. 9.7, a List of strings is converted to uppercase and searched for those that begin with "R".

```
```csharp
// Fig. 9.7: LINQWithListCollection.cs
// LINQ to Objects using a List<string>.
using System;
using System.Linq;
using System.Collections.Generic;

class LINQWithListCollection
{
    static void Main()
    {
        // populate a List of strings
        var items = new List<string>();
        items.Add("Aqua"); // add "Aqua" to the end of the List
        items.Add("Rust"); // add "Rust" to the end of the List
        items.Add("Yellow"); // add "Yellow" to the end of the List
        items.Add("Red"); // add "Red" to the end of the List
```
```

**Fig. 9.7**   LINQ to Objects using a List<string>. (Part 1 of 2.)

1. This is not required and could be implementation dependent.