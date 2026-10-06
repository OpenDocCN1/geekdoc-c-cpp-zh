# Programming Problems 331

+   11. When sorting an array using a merge sort,
   **a.** Do the recursive calls to mergeSort depend on the values in the array, the number of items in the array, or both? Explain.
   **b.** In what sort of merge are the items in the array actually swapped (that is, sorted)? Explain.

+   12. Trace the quicksort algorithm as it sorts the following array into ascending order. List the calls to quicksort and to partition in the order in which they occur.

```
20 80 40 25 60 15
```

+   13. Suppose that you remove the call to merge from the merge sort algorithm to obtain-

```
// Mystery algorithm for theArray[0..n-1]
mystery(theArray: ItemArray, n: integer): void
if (n > 1) {
    mystery(lefthalf(theArray))
    mystery(righthalf(theArray))
}
```

What does this new algorithm do?

+   14. How many recursive calls are necessary when quicksort sorts an array of size n if you use median-of-three pivot selection?

+   15. Describe an iterative version of mergeSort.

+   **a.** Trace the radix sort for this example.
   **b.** Suppose that you did not use 7 to represent 10—that is, that H10 is the 10 of hearts—and you padded the two-character strings on the right with a blank to form three-character strings. How would radix sort order the entire deck of cards in this case?

# PROGRAMMING PROBLEMS

+   1. Add a counter to the functions insertionSort and mergeSort that counts the number of comparisons that are made. Run the two functions with arrays of various sizes. What size does the difference in the number of comparisons become significant? How does this size compare with the size that the these algorithms predict?

+   2. Revise the function quickSort so that it always chooses the first item in the array as the pivot. Add a counter to the partition function counts the number of comparisons that are made. Compare the behavior of the revised version with the original, using arrays of various sizes. What size does the difference in the number of comparisons become significant? Which pivot selection strategy size the difference in the number of comparisons become significant?