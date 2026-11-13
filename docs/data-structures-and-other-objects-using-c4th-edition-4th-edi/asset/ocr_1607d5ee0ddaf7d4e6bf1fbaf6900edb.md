# Specifying Subarrays with Pointer Arithmetic

Suppose that data is an array with at least n elements. For any integer i from 0 to n, the expression (data + i) refers to the subarray that begins at data[i] and continues to the end of the array.

In the subarray, (data + i)[0] is the same as data[i]; (data + i)[1] is the same as data[i+1]; and so on.

A subarray is always part of a complete array. Changing the subarray will change the complete array.

# Mergesort

The most straightforward implementation of the divide-and-conquer approach to sorting is the mergesort algorithm. The mergesort algorithm divides the array near its midpoint, sorts the two half-arrays by recursive calls to the algorithm, and then merges the two halves to get a new sorted array of elements. The final “merging” step of the process will require some thought, so we’ll postpone that part of the implementation by assuming that we have a separate function to carry out the merging. The prototype for the merging function is shown here:

```
void merge(int data[ ], size_t n1, size_t n2);
// Precondition: data is an array (or subarray) with at least n1 + n2
// elements. The first n1 elements (from data[0] to data[n1-1]) are sorted
// from smallest to largest, and the last n2 (from data[n1] to
// data[n1 + n2 - 1]) are also sorted from smallest to largest.
// Postcondition: The first n1 + n2 elements of data have been rearranged
// to be sorted from smallest to largest.
// NOTE: If there is insufficient dynamic memory, then bad_alloc is
// thrown.
```

This merge function will be used as the last step of our mergesort. Notice that the merge function will use some dynamic memory, so there is a possibility of failure that we have indicated in the specification. Can you predict where the dynamic memory will come into play? You’ll see the answer shortly, but for now, examine the mergesort function in Figure 13.2.

The stopping case for mergesort’s recursion is when the array to be sorted consists of only one element. In this stopping case, there is no work to do because a single element does not need to be “rearranged.” On the other hand, if there is more than one element, then the mergesort function carries out these steps:

+   1. Calculate the sizes of the two subarrays. The first size, n1, is approximately half of the entire size (calculated by n/2, using integer division).
+   The second size, n2, is whatever is left over (calculated by n – n1).