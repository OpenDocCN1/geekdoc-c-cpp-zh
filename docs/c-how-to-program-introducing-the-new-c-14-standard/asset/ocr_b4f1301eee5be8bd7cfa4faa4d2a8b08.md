# # Third Iteration

On the third iteration, the program determines the next smallest value, 10, and swaps it with the value in element 2 (34).

![](bbox=[0.118, 0.238, 0.882, 0.337])

The process continues until the array is fully sorted.

![](bbox=[0.118, 0.415, 0.882, 0.515])

After the first iteration, the *smallest* element is in the *first* position; after the second iteration, the *two smallest* elements are *in order* in the *first two* positions and so on.

# # Function Template `selectionSort`

Function template `selectionSort` performs the sorting in lines 12–26. The loop iterates `size − 1` times. Line 13 declares and initializes the variable `indexOfSmallest`, which stores the index of the smallest element in the unsorted portion of the `array`. Lines 16–20 iterate over the remaining array elements. For each element, line 17 compares the current element’s value to the value at `indexOfSmallest`. If the current