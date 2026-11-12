+   11. When sorting an array by using a merge sort,
+      a. Do the recursive calls to mergeSort depend on the values in the array, the number of items in the array, or both? Explain.
+      b. In what step of mergeSort are the items in the array actually swapped (that is, sorted)? Explain.

+   12. Trace the quick sort algorithm as it sorts the following array into ascending order. List the calls to quicksort and to partition in which they occur.
+      20 80 40 25 60 10 15

+   13. Suppose that you remove the call to merge from the merge sort algorithm to obtain
+      // Mystery algorithm for theArray[0..n-1].
+      mystery(theArray: ItemArray, n: integer): void
+      if (n > 1)
+      {
+      mystery(leftHalf(theArray))
+      mystery(rightHalf(theArray))
+      }
+      What does this new algorithm do?

+   14. How many recursive calls are necessary when quickSort sorts an array of size n if you use median-of-three pivot selection?

+   15. Describe an iterative version of mergeSort.

+   16. One criterion used to evaluate sorting algorithms is stability. A sorting algorithm is stable if it does not exchange items that have the same sort key. Thus, items with the same sort key (possibly differing in other ways) will maintain their positions relative to one another. For example, you might want to take an array of students sorted by name and re-sort it by year of graduation. Using a stable sorting algorithm to sort the array by year will ensure that within each year the students will remain sorted by name. Some applications mandate a stable sorting algorithm. Others do not. Which of the sorting algorithms described in this chapter are stable?

+   17. When we discussed the radix sort, we sorted a hand of cards by first ordering the cards by rank and then by suit. To implement a radix sort for this example, you could use two characters to represent a card, if you used the letter T to represent a 10. For example, S2 is the 2 of spades and HT is the 10 of hearts.
+      a. Trace the radix sort for this example.
+      b. Suppose that you did not use T to represent a 10—that is, suppose that H10 is the 10 of hearts—and that you padded the two-character strings on the right with a blank to form three-character strings. How would a radix sort order the entire deck of cards in this case?

# PROGRAMMING PROBLEMS

+   1. Add a counter to the functions insertionSort and mergeSort that counts the number of comparisons that are made. Run the two functions with arrays of various sizes. At what size does the difference in the number of comparisons become significant? How does this size compare with the size at which the orders of these algorithms predict?

+   2. Revise the function quickSort so that it always chooses the first item in the array as the pivot. Add a counter to the function partition that counts the number of comparisons that are made. Compare the behavior of the revised function with the original one, using arrays of various sizes. At what size does the difference in the number of comparisons become significant? For which pivot selection strategy does the difference in the number of comparisons become significant?