# Sec. 7.4 Mergesort

# 243

```
template <typename E, typename Comp>
void mergesort(E A[], E temp[], int left, int right) {
    if (left = right) return;      // List of one element
    int mid = (left+right)/2;
    mergesort(E,Comp, A, temp, left, mid);
    mergesort(E,Comp, A, temp, mid+1, right); // Copy subarray to temp
    for (int i=left; i<=right; i++) {
        temp[i] = A[i];
    }
    int il = left; int ir = mid + 1;
    for (int curr=left; curr<=right; curr++) {
        if (il > mid)                // sublist exhausted
            A[curr] = temp[ir++];
        else if (ir > right)        // Right sublist exhausted
            A[curr] = temp[il++];
        else if (Comp(temp[il], temp[ir]))
            A[curr] = temp[il++];
        else
            A[curr] = temp[ir++];
    }
}
```

> Figure 7.8 Standard implementation for Mergesort.

input list alternating between the two sublists. The first element is assigned to the first sublist, the second element to the second sublist, the third to first sublist, the fourth to the second sublist, and so on. This requires one pass through the input list to build the sublists.

When the input to Mergesort is an array, splitting it into two subarrays is easy if we know the bounds. Merging is also easy if we merge the subarrays into a second array. Note that this approach requires twice the space of any of the sorting methods presented so far, which is a serious disadvantage for Mergesort. It is possible to merge the subarrays without using a second array, but it is difficult to do efficiently and not really practical. Merging the two subarrays into a second array, while simple to implement, presents another difficulty. The process ends with the sorted list in the auxiliary array. Consider how the recursive nature of Mergesort breaks the original array into subarrays, as in Figure 7.8. Mergesort is recursively called until subarrays of size 1 have been created, requiring log n levels of recursion. These subarrays are merged into subarrays of size 2, which in turn are merged into subarrays of size 4, and so on.

We need to devise an algorithm that alternates between two arrays. A much simpler approach is to copy the sorted sublists to the auxiliary array first, and then merge them back to the original array. Figure 7.9 shows a complete implementation for mergesort following this approach.

An optimized Mergesort implementation is shown in Figure 7.10. It reverses the order of the second subarray during the initial copy. Now the current positions of the two subarrays work inwards from the ends, allowing the end of each subarray