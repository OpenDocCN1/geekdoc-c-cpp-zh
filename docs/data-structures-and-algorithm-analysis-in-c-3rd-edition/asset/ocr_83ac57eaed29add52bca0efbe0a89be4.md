```
template <typename E, typename Comp>
void qsort(E A[], int i, int j) { // Quicksort
    if (j <= i) return; // Don't sort 0 or 1 element
    int pivotindex = findpivot(A, i, j);
    swap(A, pivotindex, j);     // Put pivot at end
    // k will be the first position in the right subarray
    int k = partition<E,Comp>(A, i-1, j, A[j]);
    swap(A, k, j);              // Put pivot in place
    qsort<E,Comp>(A, i, k-1);
    qsort<E,Comp>(A, k+1, j);
}
```

# Figure 7.11 Implementation for Quicksort.

placed at the end of the array (position j). Thus, partition must not affect the value of array position j. After partitioning, the pivot value is placed in position k, which is its correct position in the final, sorted array. By doing so, we guarantee that at least one value (the pivot) will not be processed in the recursive calls to qsort. Even if a bad pivot is selected, yielding a completely empty partition to one side of the pivot, the larger partition will contain at most n − 1 elements.

Selecting a pivot can be done in many ways. The simplest is to use the first key. However, if the input is sorted or reverse sorted, this will produce a poor partitioning with all values to one side of the pivot. It is better to pick a value at random, thereby reducing the chance of a bad input order affecting the sort. Unfortunately, using a random number generator is relatively expensive, and we can do nearly as well by selecting the middle position in the array. Here is a simple findpivot function:

```
template <typename E>
inline int findpivot(E A[], int i, int j)
{ return (i+j)/2; }
```

We now turn to function partition. If we knew in advance how many keys are less than the pivot, partition could simply copy elements with key values less than the pivot to the low end of the array, and elements with larger keys to the high end. Because we do not know in advance how many keys are less than the pivot, we use a clever algorithm that moves indices inwards from the ends of the subarray, swapping values as necessary until the two indices meet. Figure 7.12 shows a C++ implementation for the partition step.