
### 21.7.2 Efficiency of Merge Sort

Merge sort is a far more efficient algorithm than either insertion sort or selection sort—although that may be difficult to believe when looking at Fig. 21.5’s busy output. Consider the non-recursive first mergeSort call (line 118). This results in

- two recursive mergeSort calls with sub-arrays that are each approximately half the original array’s size, and
- a single call to merge.

The merge call requires, at worst, *n* − 1 comparisons to fill the original array, which is *O(n)*. (Recall that each array element is chosen by comparing one element from each sub-array.) The two mergeSort calls result in

- four more recursive mergeSort calls, each with a sub-array approximately one-quarter the size of the original array, and
- two calls to merge.

These two calls to merge each require, at worst, *n/2* − 1 comparisons for a total of *O(n)* comparisons. This process continues with each mergeSort call generating two additional mergeSort calls and a merge call until the algorithm has split the array into one-element sub-arrays. At each level, *O(n)* comparisons are required to merge the sub-arrays. Each level splits the arrays in half, so doubling the array size requires one more level and quadrupling the array size requires two more levels. This pattern is logarithmic, resulting in log₂ *n* levels for a total efficiency of *O(n log n)*.

### 21.7.3 Summarizing Various Algorithms’ Big O Notations

The following diagram summarizes the searching and sorting algorithms we cover in this chapter and lists the Big O for each.

| Algorithm | Location | Big O |
|---|---|---|
| *Searching Algorithms* |  |  |
| Linear search | Section 21.3 | *O(n)* |
| Binary search | Section 21.4 | *O(log n)* |
| Recursive linear search | Exercise 21.8 | *O(n)* |
| Recursive binary search | Exercise 21.9 | *O(log n)* |
| *Sorting Algorithms* |  |  |
| Insertion sort | Section 21.5 | *O(n²)* |
| Selection sort | Section 21.6 | *O(n²)* |
| Merge sort | Section 21.7 | *O(n log n)* |
| Bubble sort | Exercises 21.5–21.6 | *O(n²)* |
| Quicksort | Exercise 21.10 | Worst case: *O(n²)*<br>Average case: *O(n log n)* |

Compare these parts of the output. How are your observations consistent with how the merge sort works?

**Answer:**
- 1. In the final merge phase, each sub-array corresponds to one of the unsorted sub-arrays produced by the algorithm’s first split pass.
- 2. Each sub-array entering the final merge phase is sorted.
- 3. The 10-element final merged array contains the same elements as the original unsorted array that entered the first split pass.
- 4. The 10-element final merged array is, in fact, sorted. The recursive merge sort splits the original unsorted array into smaller and smaller pieces until they are down to single-element pieces, which it ultimately merges to form the smallest sorted pieces of the original array. It keeps merging those sorted pieces to form larger and larger sorted pieces until it finally merges the two—now sorted—halves of the original unsorted array to form the final sorted array.

## 21.8 **Wrap-Up**

This chapter discussed searching and sorting data. We began by introducing Big O notation to express the efficiency of algorithms by measuring their worst-case run times. Throughout the chapter, you saw that Big O is useful for comparing algorithm performance so you can choose the most efficient one.

Next, we discussed searching. We presented the simple but inefficient linear search algorithm. Then, we presented the binary search algorithm, which is faster but more complex than linear search.

Finally, we discussed sorting data. You learned two simple but inefficient sorting techniques—insertion sort and selection sort. Then, we presented the recursive merge sort algorithm, which is more efficient than either the insertion sort or the selection sort but more complex to program.

Thanks for reading *C++ How to Program: An Objects-Natural Approach, 11/e*. We hope that you enjoyed the book and that you found it entertaining and informative. Most of all we hope you feel empowered to apply the technologies you’ve learned to the challenges you’ll face in your career.

## Exercises

- **21.1** Fill in the blanks in each of the following statements:
  - a) A selection sort application would take approximately __________ times as long to run on a 128-element array as on a 32-element array.
  - b) The efficiency of merge sort is __________.
- **21.2** What key aspect of both the binary search and the merge sort accounts for the logarithmic portion of their respective Big Os?
- **21.3** In what sense is the insertion sort superior to the merge sort? In what sense is the merge sort superior to the insertion sort?
- **21.4** In the text, we say that after the merge sort splits the array into two sub-arrays, it then sorts these two sub-arrays and merges them. Why might someone be puzzled by our statement that “it then sorts these two sub-arrays”?
- **21.5** *(Bubble Sort)* In this exercise, you’ll implement the bubble sort algorithm, another simple but inefficient sorting algorithm. It’s called bubble sort because smaller values gradually “bubble” their way to the top of the array (that is, toward the first element) like air bubbles rising in water. It’s also called a sinking sort, as the larger values sink to the bottom (end) of the array. The technique uses nested loops to make several passes through the array. Each pass compares successive pairs of elements. If a pair is in increasing order (or the values are equal), the bubble sort leaves the values as they are. If a pair is in decreasing order, the bubble sort swaps their values in the array.

  The first pass compares the first two element values and swaps them if necessary. It then compares the second and third element values in the array and swaps them if necessary. This continues until the end of this pass compares the last two element values in the array and swaps them if necessary. After one pass, the largest value will be in the last element. After two passes, the largest two values will be in the last two elements and so on. Implement and test the bubble sort algorithm.

- **21.6 (Enhanced Bubble Sort)** Make the following modifications to improve the performance of the bubble sort you developed in Exercise 21.5:
  - a) After the first pass, the largest value is guaranteed to be located in the highest-numbered array element; after the second pass, the two highest values are “in place,” and so on. Instead of making *n* − 1 comparisons for an *n*-element array on every pass, modify the bubble sort to make only the *n* − 2 necessary comparisons on the second pass, *n* − 3 on the third pass, and so on.
  - b) The data in the array may already be in the proper order or near-proper order, so why make *n* − 1 passes (of an *n*-element array) if fewer will suffice? Modify the sort to check at the end of each pass whether any swaps have been made. If none have been made, the data is sorted, so the program should terminate. If swaps were made, at least one more pass is needed.
- **21.7 (Bucket Sort)** A bucket sort begins with a one-dimensional array of positive integers to be sorted and a two-dimensional array of integers with rows indexed from 0 to 9 and columns indexed from 0 to *n* − 1, where *n* is the number of values to be sorted. Each row of the two-dimensional array is referred to as a bucket. Write a class named `bucketSort` containing a function called sort that operates as follows:
  - a) Place each value of the one-dimensional array into a row of the bucket array based on the value’s “ones” (rightmost) digit. For example, 97 is placed in row 7, 3 is placed in row 3, and 100 is placed in row 0. This procedure is called a *distribution pass*.
  - b) Loop through the bucket array row by row, and copy the values back to the original array. This procedure is called a *gathering pass*. The new order of the preceding values in the one-dimensional array is 100, 3 and 97.
  - c) Repeat this process for each subsequent digit position (tens, hundreds, thousands, etc.).

  On the second (tens digit) pass, 100 is placed in row 0, 3 is placed in row 0 (because 3 has no tens digit), and 97 is placed in row 9. After the gathering pass, the order of the values in the one-dimensional array is 100, 3 and 97. On the third (hundreds digit) pass, 100 is placed in row 1, 3 is placed in row 0, and 97 is placed in row 0 (after the 3). After this last gathering pass, the original array is in sorted order.

  Note that the two-dimensional array of buckets is 10 times the length of the integer array being sorted. This sorting technique performs better than a bubble sort but requires much more memory—the bubble sort requires space for only one additional element.
