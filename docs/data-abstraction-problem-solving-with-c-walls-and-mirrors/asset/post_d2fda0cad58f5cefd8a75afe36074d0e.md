
# 324 CHAPTER 11 Sorting Algorithms and Their Efficiency

observations in mind. It assumes a constant MIN_SIZE that specifies the size of the smallest array on which we use a quick sort.

```
LISTING 11-5 A function that performs a quick sort

/** Sorts an array in ascending order. Uses the median-of-three pivot selection for arrays of at least MIN_SIZE entries, and uses the insertion sort for other arrays.
@pre theArray[first...] is an array.
@post theArray[first...] is sorted.
@param theArray The first element to consider in the array.
@param last The last element to consider in the Array.
void quickSort(int theArray[], int first, int last) {
    if (last - first + 1 < MIN_SIZE) {
        insertionSort(theArray, first, last);
    } else {
        // Create the partition: S1 | Pivot | S2
        int pivotIndex = partition(theArray, first, last);
        // Sort subarrays S1 and S2
        quickSort(theArray, first, pivotIndex - 1);
        quickSort(theArray, pivotIndex + 1, last);
    }
} // end quickSort
```

Analysis. The major effort in the quickSort function occurs during the partitioning step. Partitioning will require no more than n comparisons, and, like merging, it will be an O(n) task. The ideal situation occurs when the pivot moves to the center of the array, so the two subarrays are the same size. Every recursive call to quickSort performs a partition with equal-sized subarrays, the quick sort will be like a merge sort in that the recursive calls halve the array. Thus, fewer recursive calls to quickSort. In the previous analysis of the merge sort, you can conclude that there are log n or n log n levels of recursive calls to quickSort. Each call to quickSort involves m comparisons and at m exchanges, where m is the number of items in the subarray to be sorted. Clearly m ≤ n. Thus, the quick sort will be O(n log n), and this will be its best case.

Quick sort:
- case: O(n²): average
- case: O(n log n)

This ideal situation may not always occur, however. It is possible that each partition has empty subarray. Every recursive call will have nothing to do, the other call must enter n-1 entries instead of n/2. This occurs because the number decreases by only by 1 at each recursive call to quickSort, and the maximum number of recursive calls to quickSort is n. The result is n levels of recursive calls instead of n log n. Thus, in the worst case, quick sort is O(n²).

A formal analysis of the average-case behavior of a quick sort would show that it is O(n log n). While the merge sort is always O(n log n), quick sort can be faster in practice and does not the additional memory that merge sort needs for merging. Moreover, on large arrays, you can expect a quick sort to run significantly faster than an insertion sort. However, in its worst case, a quick sort will require roughly the same amount of time as an insertion sort.

The fact that quick sort's average-case behavior is better than its worst-case behavior distinguishes it from the other sorting algorithms considered in this chapter. If the original arrangement of data in the array is "random", the quick sort performs at least as well as any known algorithm that involves comparisons.

The efficiency of merge sort is somewhere between the possibilities for a quick sort: Sometimes the quick sort is faster, and sometimes the merge sort is faster. While the worst-case behavior of a merge sort is of the order of magnitude as a quick sort's average-case behavior, in most situations a quick sort will run significantly slower than the merge sort.

> Note: The choice of pivots affects the quick sort's efficiency. Some pivot-selection schemes can lead to worst-case behavior if the array is already sorted or nearly sorted. In practice, nearly sorted arrays occur more frequently than you might imagine. Fortunately, median-of-three pivot selection avoids worst-case behavior for sorted arrays.

> Note: The quick sort is often used to sort large arrays, as it is extremely fast in practice, despite its unimpressive theoretical worst-case behavior. Although a worst-case situation is not typical, even if the worst case occurs, the quick sort's performance is acceptable for moderately large arrays.

> Note: The quick sort is appropriate when you are confident that the data in the array to be sorted arranged randomly. Although the quick sort's worst-case behavior is O(n²), the worst case rarely occurs in practice.

# ASIDE: Quick sort versus merge sort and kSort

The QuickSort and mergeSort algorithms are similar in spirit, but whereas QuickSort does its work before its recursive calls, mergeSort does its work after its recursive calls. That is, while quickSort has the form

```
quickSort(theArray, first, last)
if (first < last)
  Prepare array for recursive calls
  quickSort(S, region of theArray)
```

(continues)

```
quickSort(S, region of theArray)
}
```

mergeSort(theArray, first, last) has the general form

```
mergeSort(theArray, first, last)
if (first < last)
    mergeSort(Left half of theArray)
    mergeSort(Right half of theArray)
    Tidy up after the recursive calls
```

The partition in quickSort is to partition the array into regions S and S'. The algorithm then sorts S and S'. In mergeSort, on the other hand, no work is done before the recursive calls: it must merge the halves. That is, the algorithm must merge the halves of the array after the recursive calls.

Now recall the pseudocode for ksmall:

```
ksmall(k, theArray, first, last):
    Choose a pivot p from theArray[first...last]
    Partition theArray[first...last] into S and S'
    if (k < pivotIndex - 1)
        return ksmall(k, theArray, first, pivotIndex - 1)
    else if (k == pivotIndex - 1)
        return p
    else
        return ksmall(k, theArray, pivotIndex + 1, last)
```

The recursive calls to ksmall act only on the section of the array. Figure 11-13 illustrates this.

> Question: Suppose that you sort a large array of integers using merge sort. Next, you use binary search to determine whether a given integer occurs in the array.
> * Which algorithm is faster, in general: the merge sort or binary search? Explain in terms of O notation.
> * Which algorithm is faster, in general: the quick sort? Explain in terms of O notation.

# Faster Sorting Algorithms 325

FIGURE 11-13 kSmall versus quickSort
(img/d0cb6b2f18b2db56996ad7c743510e_353.png)

## 11.2.3 Radix Sort

The radix sort is included here because it is quite different from the other sorts described, as it does not compare the array entries. Imagine that you are sorting a hand of cards. You pick the cards one a time and arrange them by rank into 13 possible groups: 2, 3...10, J, Q, A. Combine these groups and place the cards on the table so that the 2s are on top and the aces are on the bottom. Now pick up the cards one a time and sort them into four groups: clubs, diamonds, hearts, and spades. When taken together, the groups result in a sorted hand of cards.

A radix sort uses this idea of forming groups and then combining them to sort a collection of data. The sort treats each item as a character string. As a first example of radix sort, consider this collection of three-letter strings:

ABC, YWZ, BWZ, AAC, RLT, JBX, RDT, KLT, AEO, TLJ

The sort begins by organizing the data according to the rightmost (least significant) letters. Although none of the strings ends in A or B, you place these strings into a group. Continuing through the alphabet, you perform the following:

(ABC, AAC) (TLJ) (AEO) (RLT, RDT, KLT, JBX) (XYZ, BWZ)

The strings in each group end with the same letter, and the groups are ordered by letter. In addition, the strings within each group retain their relative order from the original list of strings.

Now combine the groups into one as follows. Take the items in the first group in their present order, follow them with the items in the second group, and so on. The following group results:
ABC, AAC, TLI, AEO, RLT, RDT, KLT, JBX, XYZ, BWZ

> Group strings by their rightmost letter

> Combine the groups

Next, form new groups as you did before, but this time use the middle letter of each string instead of the last letter:
