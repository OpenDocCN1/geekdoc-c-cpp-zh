# Chapter 7 Searching

It's still important to understand searching algorithms work, however, because sometimes you can do even better than the tools. For example, interpolation search is much faster than binary search when it is applicable.

# Linear Search

As you may be aware, a linear or exhaustive search simply loops through the items in the array, looking for the target item. Figure 7-1 shows a linear search for the value 77.

![](bbox=[0.137, 0.298, 0.703, 0.356])

Figure 7-1: a linear search examines every item in the array until it finds the target.

Unlike binary search and interpolation search, linear search works on linked lists, where you cannot easily jump from one part of the list to another, as you can in an array.

Linear search also works on unsorted lists. But if the items are sorted, the algorithm can stop if it comes to an item with a value greater than the target value. That lets the algorithm stop early and save a little time if the target isn't in the list.

The following pseudocode shows the linear search algorithm for an array:

```
// Find the target item's index in the sorted array.
// If the item isn't in the array, return -1.
Integer: LinearSearch(Data values[], Data target)
For i = 0 To <length of values> > 1
  // See if this is the target.
  If (values[i] == target) Then Return i

  // See if we have passed where the target would be.
  If (values[i] > target) Then Return -1
Next i

// If we get here, the target is not in the array.
Return -1
EndLinearSearch
```

This algorithm may need to loop through the entire array to conclude that an item isn't, so its worst-case behavior is O(N).

Even in the average case, the algorithm's run time is O(N). If you add the number of steps required to search for every item in the array, you get