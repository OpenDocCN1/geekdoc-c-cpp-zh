![](bbox=[0.166, 0.141, 0.834, 0.498])

**Fig. 2.1.5.** | Sorting an array into ascending order with merge sort. (Part 5 of 5.)

# Function mergeSort

The merge function is defined before mergeSort, so mergeSort can call it, but let’s discuss mergeSort first. The recursive mergeSort function (lines 74–97) receives as parameters the array to sort and the low and high indices of the range of elements to sort. Line 77 tests the base case. If the high index minus the low index is 0, the sub-array has one element, so the function simply returns. If the difference between the indices is greater than or equal to 1, the function splits the array in half—lines 78–79 determine the split point. Next, line 91 recursively calls mergeSort on the array’s first half, and line 92 recursively calls mergeSort on the array’s second half. When these two calls return, each half is sorted. Line 95 calls merge (lines 24–71) on the two halves to combine the sorted sub-arrays into one larger sorted array.

# Function merge

Lines 40–49 in merge loop until the program reaches the end of either sub-array. Line 40 tests which element at the beginning of the two sub-arrays is smaller. If the element in the left sub-array is smaller or both are equal, line 44 places it in position in the combined array. If the element in the right sub-array is smaller, line 47 places it in position in the combined array. When the while loop completes, one entire sub-array is in the combined array, but the other sub-array still contains data. Line 51 tests whether the left sub-array has reached the end. If so, lines 52–54 fill the combined array with the elements of the right sub-array. If the left sub-array has not reached the end, then the right sub-array must have reached the end, and lines 57–59 fill the combined array with the elements of the left sub-array. Finally, lines 63–65 copy the combined array into the original array.