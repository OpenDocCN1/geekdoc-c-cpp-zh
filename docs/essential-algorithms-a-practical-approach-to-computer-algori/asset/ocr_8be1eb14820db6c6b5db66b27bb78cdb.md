# Appendix B ■ Solutions to Exercises 511

+   5. Example program Bubblesort implements the bubblesort algorithm.

+   6. Example program ImprovedBubblesort adds some improvements.

+   7. Example program PriorityQueue uses a heap to implement a priority queue. (This program works directly with the value and priority arrays. For more practice, package the heap code into a class.)

+   8. Adding an item and removing an item from a heap containing N items takes O(log N) time. See the discussion of the heapsort's run time for details.

+   9. Example program Heapsort implements the heapsort algorithm.

+   10. For a complete tree of degree d, if a node has index p, its children are at d \times p + 1, d \times p + 2, and a node at index p has index [(p - 1)] / d.

+   11. Example program QuicksortStack implements the quicksort algorithm with stacks.

+   12. Example program QuicksortQueue implements the quicksort algorithm with queues. Stacks and queues provide the same performance as the quicksort algorithm is concerned. Any difference would be in the stacks and queues implemented.

+   13. Example program Quicksort implements the quicksort algorithm with in-place partitioning.

+   14. Instead of dividing the items into halves at each step, divide them into three groups. The first group contains items strictly less than the dividing item, the middle group contains all repetitions of the dividing item, and the last group contains items greater than the dividing item. Recursively sort the first and third groups not the second.

+   15. Example program Countingsort implements the countsort algorithm.

+   16. Allocate a count array with indices 0 to 10,000. Subtract the smallest value (100,000) from each item before you increment its count. Then, when you are writing the counts back into the original array, add 100 back in. (Alternatively, you could use an array with nonzero lower bounds, as described in Chapter 4.) Sortort each bucket, but all the items in a particular bucket would have the same value. As the buckets don't hold too many items, that's not a problem, but countsort still has a small advantage, because it only needs to count the items in each bucket.

+   17. Example program Bucketsort implements the bucketsort algorithm.

+   18. The following paragraphs explain which algorithms would work well under the indicated circumstances.

+   a. 10 floating-point numbers—Any of the algorithms except countsort would work. Insertionsort, selectionsort, and bubblesort would be simplest and probably provide the best performance.

+   b. 100 integers—Heapsort, quicksort, and mergesort would work well. Quicksort would be fastest if the items don't contain too many duplicates and are not initially sorted or you use a randomized method for dividing items. Countingsort would work if the range of values is limited.