
## CHAPTER 11 Sorting Algorithms and Their Efficiency

The partition function will receive a segment array `array[first..last]` as an argument. The function must arrange the items of the array segment into two regions: $S_1$ contains the items less than or equal to the pivot and $S_2$ contains the items greater than the pivot. Thus, as you see in Figure 11-9, the segment is `array[first..pivotIndex]`, and $S_2$ is the segment `array[pivotIndex + 1..last]`.

What would you choose? Various strategies exist for making this choice, as you will see later, let's assume for now that we have a pivot and go to develop the partition. Regardless of which pivot you choose, let's swap it with the last entry `array[last]` to get out of the way we partition the array. Figure 11-10 shows an array after this step. Starting at the beginning of the array and moving towards the (left to right), look for the first entry that is greater than or equal to the pivot. In Figure 11-10, that entry is 5 which occurs at the `indexFromLeft`. In a similar fashion, starting at the next-to-last entry and moving towards the beginning of the array (right to left in the figure), look for the first entry that is less than equal to the pivot. In Figure 11-10b, that entry is 2 and occurs at the `indexFromRight`. Now, if `indexFromLeft` is less than `indexFromRight`, swap the two entries at those indices. Figure 11-10c shows the result of this step. The two is less than the pivot, has moved toward the beginning of the array, while the 5, is greater than the pivot, has moved in the opposite direction.

Place your chosen pivot in the `array[last]` before partitioning

# FIGURE 11-10 A partitioning of an array during a quick sort

![](img/d0cb86b2f18b2db569968ad7c743510e_346_0.png)

Continue the searches from the left and from the right. Figure 11-10d shows that the search from the left stops at 4 and the search from right stops at 1. `indexFromLeft` is less than `indexFromRight`, swap 4 and 1. The array now appears as in Figure 11-10. Entries equal to the pivot are allowed in either piece of the partition.

Continue the searches. Figure 11-1f shows that the search from the left stops at 6, while from the right goes beyond the 6 to stop at 1. `indexFromLeft` is not less than `indexFromRight`, no swap is necessary and the ends. The only remaining step is to place pivot between subarrays $S_i$ and $S_j$, by swapping $a[indexFromLeft]$ and $a[last]$, as Figure 11-10g shows. The completed partition appears in Figure 11-10h.

Note that the previous subarrays must not go beyond the ends of the array. You will see a convenient way to implement this requirement.

**Entries equal to the pivot.** Note that both of the subarrays $S_i$ and $S_j$ can contain entries equal to the pivot. This might seem a strange to you. Why not always place entries that equal the pivot to the same subarray? Such a strategy would make one subarray larger than the other. However, to enhance the quick sort's performance, we want the subarrays to be nearly equal as possible.

Notice that both search from the left and the search from the right stop when they encounter an entry that equals the pivot. This means that when leaving entries in subarrays, they are swapped. It also means that each search has an entry of landing in each of the subarrays.

**Selecting a pivot.** Ideally, the pivot should be the median value in the array, so that the subarrays $S_i$ and $S_j$, each have the same—or nearly the same—number of entries. One way to find the median value is to sort the array and then get the value in the middle. But sorting this logic is doomed. Instead of getting the best pivot by finding the median of all values in the array, we will all try to avoid a bad pivot. 

We will pick the median of three entries in the array: the first entry, the middle entry, the last entry. One way to accomplish this is to sort only these three entries and use the middle of the three as the pivot. Figure 11-11 shows an array before and after its first, middle, and last entries are sorted. The pivot is 5. This pivot selection strategy is called **median-of-three pivot selection.**

This pivot selection ensures that the array has three entries. If you have only three entries, the pivot selection sorts them, so there is no need for the partition method or for a quick sort. we now assume that the array contains at least four entries.

The following pseudocode describes how to sort the first, middle, and last entries in an array of least four entries. For example, it will transform the array in Figure 11-11a to the one in Figure 11-11b.

![](img/d0cb86b2f18b2db569968ad7c743510e_347_0.png)

| | 5 | 8 | 6 | 4 | 9 | 3 | 7 | 1 | 2 |
|---|---|---|---|---|---|---|---|---|---|
| (b) | 2 | 8 | 6 | 4 | 5 | 3 | 7 | 1 | 9 |
| Pivot | | | | | | | | | |

| | 5 | 8 | 6 | 4 | 9 | 3 | 7 | 1 | 2 |
|---|---|---|---|---|---|---|---|---|---|
| (a) | 5 | 8 | 6 | 4 | 9 | 3 | 7 | 1 | 2 |
| (b) | 2 | 8 | 6 | 4 | 5 | 3 | 7 | 1 | 9 |

```cpp
// Sort the first, middle, and last entries in an array into ascending order.
sortFirstMiddleLast(array: ItemArray, first: integer, mid: integer, last: integer): void
    if (array[first] > array[mid])
        Interchange(array[first] and array[mid])
    if (array[mid] > array[last])
        Interchange(array[mid] and array[last])
```

Adjusting the partition algorithm. Median-of-three pivot selection suggests some adjustments to our partitioning scheme. Previously, we swapped the pivot with the last entry in the array prior to partitioning. But here the first, middle, and last entries are sorted, so we know that the last entry is least as large as the pivot. To get the pivot out of the way, we can swap it with the next-to-last entry, a[last-1], as Figure 11-12 shows. Therefore, the partition algorithm can begin its search from the right at last-2.

Also notice that the first entry is least as small as the pivot, and it lies in the subarray $S_f$. We can then leave the last entry in place and have the partition algorithm begin its search from the left at first+1. Figure 11-12b shows the status of the array at this point, just prior to partitioning. This scheme provides a side benefit that simplifies the loops for the two searches. The search for the entry that is greater than or equal to the pivot. That search will terminate, at worst, will stop at the pivot. The search from the right looks for an entry less than or equal to the pivot. That search will terminate, at worst, will stop at the first entry. Thus, the loops need not do anything special to prevent the searches from going beyond the ends of the array.

After the search loops end, we need to position the pivot between the subarrays $S_f$ and $S_l$. We do this by swapping the entries at `indexFromLeft` and `last-1`.

Note: The quick sort rearranges the entries in an array during the partitioning process. Each partition places one entry—the pivot—in its correct sorted position. The entries in each of the two subarrays before and after the pivot will remain in their respective subarrays.

The following pseudocode describes the partitioning algorithm for an array of least four entries: The partition algorithm

```cpp
// Partitions array[...last].
partition(array: ItemArray, first: integer, last: integer): integer
    // Choose pivot and position
    mid = first + (last - first) / 2
    sortFirstMiddleLast(array, first, mid, last)
    Interchange(array[mid] and array[last - 1])
    pivotIndex = last - 1
    pivot = array[pivotIndex]
    // Determine the regions S1 and S2
    indexFromLeft = first + 1
    indexFromRight = last - 2

    done = false
    while (not done) {
      // Locate first entry on left that is >= pivot
      while (array[indexFromLeft] < pivot)
        indexFromLeft = indexFromLeft + 1
      // Locate first entry on right that is <= pivot
      while (array[indexFromRight] > pivot)
        indexFromRight = indexFromRight - 1
      if (indexFromLeft < indexFromRight) {
        // Move array[indexFromLeft] into S2
        Interchange(array[indexFromLeft] and array[indexFromRight])
        indexFromLeft = indexFromLeft + 1
        indexFromRight = indexFromRight - 1
      } else {
        done = true
      }
    }
    // Place pivot in proper position between S1 and S2, and mark its new location
    Interchange(array[pivotIndex] and array[indexFromLeft])
    pivotIndex = indexFromLeft
    return pivotIndex
```

- **Question 9** Trace the quick sort's partitioning algorithm as it partitions the array: 38 16 40 39 12 27

**A function for the quick sort.** Before completing the C++ code for quick sort, we need to think about small arrays. You have seen that the array should contain at least four entries before you call the partition method. By simply using the quick sort only on large arrays is not enough. The code will eventually lead to a recursive call that involves an array as small as two entries. The code for the quick sort needs to screen out these small arrays and use another way to sort them. Insertion sort is a good choice for small arrays. In fact, using insertion sort instead of the quick sort on arrays of as small as ten entries is reasonable. The function in Listing 11-5 implements the quick sort with these
