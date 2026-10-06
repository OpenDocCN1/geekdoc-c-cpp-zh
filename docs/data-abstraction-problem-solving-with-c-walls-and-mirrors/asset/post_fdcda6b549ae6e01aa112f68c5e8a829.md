
## Faster Sorting Algorithms 315

```
// Merge sorted halvesArray[first..mid] and theArray[mid+1..]
merge(theArray, first, mid, last)
}
// If first >= last, there is nothing to do
```

Clearly, most of the effort in the merge sort is in the merge step, but does this algorithm actually sort? The recursive calls continue dividing the array into the pieces until each piece contains only one item; obviously an array of one item is sorted. The algorithm then merges these small pieces into larger sorted pieces until one sorted array results. Figure 11-6 illustrates the recursive calls and the merge steps in a sort of an array of six.

The C++ functions in Listing 11-4 implement the merge sort algorithm. To sort an array theArray of n items, you would invoke the function mergeSort by writing

```
mergeSort(theArray, 0, n - 1);
```

## FIGURE 11-6 A merge sort of an array of six integers

![](img/d0cb86b2f18b2db569968ad7c743510e_341_0.png)

## LISTING 11-4 An implementation of the merge sort

```cpp
const int MAX_SIZE = maximum-number-of-items-in-array;
/**
 * Merges sorted array segments theArray[first..mid] and
 * theArray[mid+1..last] into one sorted array.
 * @param first first < mid <= last. The subarrays theArray[first..mid] and
 * theArray[mid+1..last] are each sorted in increasing order.
 * @post theArray[first..last] is sorted.
 * @param theArray The given array.
 * @param first The index of the beginning of the first segment in
 * theArray.
 * @param mid The index of the end of the first segment in theArray;
 * mid + 1 marks the beginning of the second segment.
 * @param last The index of the last element in the second segment in
 * theArray.
```

(continues)

## 316 CHAPTER 11 Sorting Algorithms and Their Efficiency

```cpp
// Note This merges the two subarrays into a temporary array
// and copies the result into the original arrayArray. */
void merge(ItemTypeArray[], int first, int mid, int last)
{
    ItemType tempArray[MAX_SIZE]; // Temporary array

    // Initialize the local indices to indicate the subarrays
    int first1 = first; // Beginning of first subarray
    int last1 = mid; // End of first subarray
    int first2 = mid + 1; // Beginning of second subarray
    int last2 = last; // End of second subarray

    // While both subarrays are not empty, copy the
    // smaller item into the temporary array
    int index = first; // Next available location in tempArray
    while ((first1 <= last1) && (first2 <= last2))
    {
        // At this point, tempArray[index-1] is in order
        if (array[first1] <= array[first2])
        {
            tempArray[index] = array[first1];
            first1++;
        }
        else
        {
            tempArray[index] = array[first2];
            first2++;
        } // and if
        index++;
    } // end while

    // Finish off the first subarray, if necessary
    while (first1 <= last1)
    {
        // At this point, tempArray[index-1] is in order
        tempArray[index] = array[first1];
        first1++;
        index++;
    } // end while

    // Finish off the second subarray, if necessary
    while (first2 <= last2)
    {
        // At this point, tempArray[index-1] is in order
        tempArray[index] = array[first2];
        first2++;
        index++;
    } // end while

    // Copy the result back into the original array
    for (index = first; index <= last; index++)
        array[index] = tempArray[index];
} // end merge
```

```cpp
/* Sorts the items in an array into ascending order.
 * @pre theArray[first..last] is an array.
 * @post theArray[first..last] is sorted in ascending order.
 * @param theArray The Index of the first element to consider in theArray.
 * @param last The Index of the last element to consider in theArray. */
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

![](img/d0cb86b2f18b2db569968ad7c743510e_343_0.png)

**Question 7** By drawing a diagram like the one shown in Figure 11-6, trace the merge sort as it sorts the following array into ascending order: 25 30 20 80 40 60.

**Question 8** Show that the merge sort algorithm satisfies the four criteria of recursion in Chapter 2 describes.

Analysis. Because the merge sort requires the most effort, let's begin the analysis. Each merge sort merges theArray[first..mid] and theArray[mid+1..last]. Figure 11-7 provides an example of a merge step that requires the maximum number of comparisons. If the total number of items in the array to be merged is $n$, then merging the segments requires $n-1$ comparisons. (For example, in Figure 11-7 seven items are in the segments and five comparisons

## FIGURE 11-7 A worst-case instance of the merge step in a merge sort

| | | | | | | |
|---|---|---|---|---|---|---|
| theArray: | 1 | 2 | 8 | 4 | 5 | 6 |
| | a | b | c | d | e | f |
| tempArray: | 1 | 2 | 4 | 5 | 6 | |

## 314 CHAPTER 11 Sorting Algorithms and Their Efficiency

## FIGURE 11-8 Levels of recursive calls, each of the array

![](img/d0cb86b2f18b2db569968ad7c743510e_344_0.png)

## 315 Faster Sorting Algorithms

## FIGURE 11-9 A partition about a pivot

![](img/d0cb86b2f18b2db569968ad7c743510e_345_0.png)

## 11.2 Quick Sort

The quick sort partitions an array into items that are less or equal to the pivot and that are greater than or equal to the pivot.
