# TABLE 18-10  Analysis of the Quick Sort Algorithm for a List of Length *n*

|  | Number of Comparisons | Number of Swaps |
|---|---|---|
| Average case | (1.39) log₂ *n* + O(*n*) = O(*n* log₂ *n*) | (0.69) log₂ *n* + O(*n*) = O(*n* log₂ *n*) |
| Worst case | *n*²/2 − *n*/2 = O(*n*²) | *n*²/2 + 3*n*/2 − 2 = O(*n*²) |

# Merge Sort: Linked List-Based Lists

In the previous section, we described the quick sort algorithm and stated that the average-case behavior of a quick sort is O(*n*log₂*n*). However, the worst-case behavior of a quick sort is O(*n*²). This section describes the sorting algorithm whose behavior is always O(*n*log₂*n*).

Like the quick sort algorithm, the merge sort algorithm uses the divide-and-conquer technique to sort a list. A merge sort algorithm also partitions the list into two sublists, sorts the sublists, and then combines the sorted sublists into one sorted list. This section describes the merge sort algorithm for linked list-based lists. We leave it for you to develop the merge sort algorithm for array-based lists, which can be done by using the techniques described for linked lists.

The merge sort and the quick sort algorithms differ in how they partition the list. As discussed earlier, a quick sort first selects an element in the list, called pivot, and then partitions the list so that the elements in one sublist are less than pivot and the elements in the other sublist are greater than or equal to pivot. By contrast, a merge sort divides the list into two sublists of nearly equal size. For example, consider the list whose elements are as follows:

```
```text
list: 35  28  18  45  62  48  30  38
```
```

The merge sort algorithm partitions this list into two sublists as follows:

```
```text
first sublist: 35  28  18  45
second sublist: 62  48  30  38
```
```

The two sublists are sorted using the same algorithm (that is, a merge sort) used on the original list. Suppose that we have sorted the two sublists. That is, suppose that the lists are now as follows:

```
```text
first sublist: 18  28  35  45
second sublist: 30  38  48  62
```
```

Next, the merge sort algorithm combines, that is, merges, the two sorted sublists into one sorted list.

Figure 18–30 further illustrates the merge sort process.