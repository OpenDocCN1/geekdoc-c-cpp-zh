```
/* Sorts the items in an array into ascending order.\n@pre theArray[first..last] is an array.
@post theArray[first..last] is sorted in ascending order.
@param theArray The Index of the first element to consider in theArray.
@param last The Index of the last element to consider in theArray.*/
void mergeSort(intType theArray[], int first, int last) {
    if (first < last) {
        // Sort each half
        int mid = first + (last - first) / 2; // Index of midpoint
        // Sort left half theArray[first..mid]
        mergeSort(theArray, first, mid);
        // Sort right half theArray[mid+1..last]
        mergeSort(theArray, mid + 1, last);
        // merge the two halves
        merge(theArray, first, mid, last);
    } // end if
}
```

![](bbox=[0.068, 0.492, 0.114, 0.532])

**Question 7** By drawing a diagram like the one shown in Figure 11-6, trace the merge sort as it sorts the following array into ascending order: 25 30 20 80 40 60.

**Question 8** Show that the merge sort algorithm satisfies the four criteria of recursion in Chapter 2 describes.

Analysis. Because the merge sort requires the most effort, let's begin the analysis. Each merge sort merges theArray[first..mid] and theArray[mid+1..last]. Figure 11-7 provides an example of a merge step that requires the maximum number of comparisons. If the total number of items in the array to be merged is $n$, then merging the segments requires $n-1$ comparisons. (For example, in Figure 11-7 seven items are in the segments and five comparisons

# FIGURE 11-7 A worst-case instance of the merge step in a merge sort

| | | | | | |
|---|---|---|---|---|---||
| theArray: | 1 | 2 | 8 | 4 | 5 | 6 |
| | a | b | c | d | e | f |
| tempArray: | 1 | 2 | 4 | 5 | 6 | 8 |