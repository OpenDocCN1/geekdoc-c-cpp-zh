| Unsorted List | 56 | 91 | 35 | | 72 | 48 | 68 |
|---|---|---|---|---|---|---|---|
| | 56 | 91 | 35 | | 72 | 48 | 68 |
| | 35 | 91 | 56 | | 72 | 48 | 68 |
| | 35 | 72 | 56 | 91 | 48 | 48 | 68 |
| | 35 | 72 | 56 | 48 | 91 | 91 | 68 |
| | 35 | 72 | 56 | 48 | 68 | 68 | 91 |
| | 35 | 68 | 56 | 48 | 72 | 72 | 91 |
| | 35 | 56 | 68 | 48 | 48 | 72 | 91 |
| | 35 | 56 | 48 | 48 | 68 | 72 | 91 |
| Sorted List | 35 | 48 | 56 | 68 | 72 | 91 |

# Fig. 5.4 : Trace of a quick sort.

The pivot selected should be such that it is smaller than about half the elements and larger than about half the elements. Consider the extreme case where either the smallest or the largest value is chosen as the pivot. When quick sort is called recursively on the values on either side of it, one set of data will be empty while the other would be almost as large as the original data set. If a bad pivot element is chosen, the array will not be evenly, divided and quick sort may be called on an array that is just as big as the original array.

In the best case, quick sort is said to be O(n log n) and this case occurs when the input array is evenly divided. In the worst case, the timing of the quick sort is O(n^2). This case occurs when the pivot element fails to divide the input array at all (i.e., all elements are greater than or smaller than the pivot element). To improve the efficiency of the sort, there are clever ways to choose the pivot value such that it is extremely unlikely to end up with an extreme value. One such method is called the median-of-three partitioning. In this method, three elements are randomly chosen and the median of these three values is chosen as the pivot element.

# 5.8 Hashing

Hashing is a data structure that allows insertion, deletion and search operations to be carried out in O(1) time. However, hashing is not efficient in operation that requires any ordering information among the elements, such as sorting, finding minimum and maximum element.

Let us assume we need to keep information about 500 students. Hence, we can assign an identification number to each student between 0 and 499 and then use a multidimensional array of 500 elements. Accessing elements in an array is extremely efficient. Array elements are usually accessed by index (also referred as its subscript). To search for a particular