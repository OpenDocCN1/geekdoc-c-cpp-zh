# Chapter 9 Introduction to LINQ and the List Collection

statements. When Line 81 executes, however, Count and Capacity are both 4, so the List doubles its Capacity to 8 and the Count becomes 5, leaving room for three more elements.

# Doubling the Capacity

When a List grows, it must (behind the scenes) create a larger internal array and copy each element to the new array. This is a time-consuming operation. It would be inefficient for the List to grow each time an element is added. To minimize of memory reallocations, a List doubles its capacity when more memory is required.

> Performance Tip 9.1
Doubling a List's Capacity is an efficient way for a List to grow quickly to the right size. This operation is more efficient than growing a List by only as much space as it takes to hold the element(s) being added. A disadvantage is that the List might occupy more space than it requires. This is a classic example of the spacetime trade-off.

> Performance Tip 9.2
It can be wasteful to double a List when more space is needed. For an example, a List of 1,000,000 elements resizes to 2,000,000 elements when one element is added. This wastes 999,999 elements. You can use Trim() to reduce a List's Capacity to its current Count. You can also set the Capacity to directly control space usage better—or if your List will never grow beyond 100 elements, you can preallocate that space by assigning 100 to the List's Capacity or using the List constructor that receives an initial capacity.

# 9.5 Querying the Generic List Collection using LINQ

As arrays, we use LINQ to Objects to query groups Lists. In Fig. 9.7, a List of strings is converted to objects and searched for those that begin with "R".

```
// Fig. 9.7: LINQWithListCollection.cs
// LINQ to Objects using a List<string>
using System;
using System.Linq;
using System.Collections.Generic;

class LINQWithListCollection
{
    static void Main()
    {
        var items = new List<string>();
        items.Add("Aqua"); // add "Aqua" to the end of the List
        items.Add("Rust"); // add "Rust" to the end of the List
        items.Add("Yellow"); // add "Yellow" to the end of the List
        items.Add("Red"); // add "Red" to the end of the List
```

Fig. 9.7 | LINQ to Objects using a List<string>. (Part I of 2.)

+   1. This is not required and could be implemented demonstrated.