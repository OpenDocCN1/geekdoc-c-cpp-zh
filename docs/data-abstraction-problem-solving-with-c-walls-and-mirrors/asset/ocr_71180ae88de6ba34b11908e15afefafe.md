# Faster Sorting Algorithms 223

The following pseudocode describes the partitioning algorithm for an array of least four entries: The partition algorithm

```
// Partitions theArray[...last].
partition(theArray: ItemArray, first: integer, last: integer): integer
// Choose pivot and position in
mid = first + (last - first) / 2
sortFirstMiddleLast(theArray, first, mid, last)
Interchange theArray[mid] and theArray[last - 1]
pivotIndex = last - 1
pivot = theArray[pivotIndex]
// Determine the regions S1 and S2
indexFromLeft = first + 1
indexFromRight = last - 2

done = false
while (not done) {
  // Locate first entry on left that is >= pivot
  while (theArray[indexFromLeft] < pivot)
    indexFromLeft = indexFromLeft + 1
  // Locate first entry on right that is <= pivot
  while (theArray[indexFromRight] > pivot)
    indexFromRight = indexFromRight - 1
  if (indexFromLeft < indexFromRight) {
    Move theArray[firstUnknown] into S2
    Interchange theArray[indexFromLeft] and theArray[indexFromRight]
    indexFromLeft = indexFromLeft + 1
    indexFromRight = indexFromRight - 1
  } else {
    done = true
  }
}
// Place pivot in proper position between S1 and S2, and mark its new location
Interchange theArray[pivotIndex] and theArray[indexFromLeft]
pivotIndex = indexFromLeft
return pivotIndex
```

+   **Question 9** Trace the quick sort's partitioning algorithm as it partitions the array: 38 16 40 39 12 27

**A function for the quick sort.** Before completing the C++ code for quick sort, we need to think about small arrays. You have seen that the array should contain at least four entries before you call the partition method. By simply using the quick sort only on large arrays is not enough. The code will eventually lead to a recursive call that involves an array as small as two entries. The code for the quick sort needs to screen out these small arrays and use another way to sort them. Insertion sort is a good choice for small arrays. In fact, using instead of the quick sort on arrays of as as ten entries is reasonable. The function in Listing 11-5 implements the quick sort with these