```
template <typename E, typename Comp>
void mergesort(E A[], E temp[], int left, int right) {
    if ((right-left) <= THRESHOLD) { // Small list
        insort(E,Comp, &A[left], right-left+1);
        return;
    }
    int i, j, k, mid = (left+right)/2;
    mergesort(E,Comp, A, temp, left, mid);
    mergesort(E,Comp, A, temp, mid+1, right);
    // Do the merge operation. First, copy two halves to temp.
    for (i=left; i<=mid; i++) temp[i] = A[i];
    for (j=mid+1; j<=right; j++) temp[j] = A[j]; // Note below
    // Merge subarrays back to A
    for (i=left, j=mid+1, k=left; k<=right; k++) {
        if (Comp::prior(temp[i], temp[j])) A[k] = temp[i++];
        else A[k] = temp[j--];
    }
}
```

# Figure 7.10 Optimized implementation for Mergesort.

to act as the sentinel. Unlike the previous implementation, no test is needed to check when one of the two subarrays becomes empty. This version also uses Insertion Sort to sort small subarrays.

Analysis of Mergesort is straightforward, despite the fact that it is a recursive algorithm. The merging part takes time Θ(n) where n is the total length of the two subarrays. The array to be sorted is repeatedly split in half until subarrays of size 2 are reached, at which time they are merged to size 2, these merged to subarrays of size 4, and so on as shown in Figure 7.8. Thus, the depth of recursion is log n (for simplicity that n is a power of two). The first level of recursion can be thought of as working on one array of size n, the next level on two arrays of n/2, the next on four arrays of n/4, and so on. At the bottom of the recursion has n arrays of size 1. Thus, n arrays of size 1 (requiring Θ(n) steps), n/2 arrays of size 2 (again requiring Θ(n) steps), n/4 arrays of size 4, and so on. At each of the log n levels of recursion, Θ(n) work is done, for a total cost of Θ(n log n). This cost is unaffected by the relative order of the values being sorted, thus this analysis holds for the best, average, and worst cases.

# 7.5 Quicksort

While mergesort uses the most obvious form of divide and conquer (split the list in half then sort the halves), it is not the only way that can break down the sorting problem. And we saw that the merging step for Mergesort when using an array implementation is not so easy. Perhaps a different divide and conquer strategy might turn out to be more efficient?