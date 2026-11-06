first power of 2 greater than the number of elements in the vector, which is represented as log₂ n. All logarithms grow at roughly the same rate, so in Big O notation the base can be omitted. This results in a Big O of O(log n) for a binary search, which is also known as logarithmic runtime and pronounced “on the order of log n” or more simply “order log n.”

# ### 19.3 Sorting Algorithms

Sorting data (i.e., placing the data into some particular order, such as ascending or descending) is one of the most important computing applications. A bank sorts all of its checks by account number so that it can prepare individual bank statements at the end of each month. Telephone companies sort their lists of accounts by last name and, further, by first name to make it easy to find phone numbers. Virtually every organization must sort some data, and often, massive amounts of it. Sorting data is an intriguing, computer-intensive problem that has attracted intense research efforts.

An important point to understand about sorting is that the end result—the sorted vector—will be the same no matter which algorithm you use to sort the vector. The choice of algorithm affects only the runtime and memory use of the program. In previous chapters, we introduced the selection sort and insertion sort—simple algorithms to implement, but inefficient. The next section examines the efficiency of these two algorithms using Big O notation. The last algorithm—merge sort, which we introduce in this chapter—is much faster but is more difficult to implement.

# #### 19.3.1 Efficiency of Selection Sort

Selection sort is an easy-to-implement, but inefficient, sorting algorithm. The first iteration of the algorithm selects the smallest element in the vector and swaps it with the first element. The second iteration selects the second-smallest element (which is the smallest element of the remaining elements) and swaps it with the second element. The algorithm continues until the last iteration selects the second-largest element and swaps it with the second-to-last element, leaving the largest element in the last index. After the i-th iteration, the smallest i elements of the vector will be sorted into increasing order in the first i elements of the vector.

The selection sort algorithm iterates n − 1 times, each time swapping the smallest remaining element into its sorted position. Locating the smallest remaining element requires n − 1 comparisons during the first iteration, n − 2 during the second iteration, then n − 3, ..., 3, 2, 1. This results in a total of n(n − 1)/2 or (n² − n)/2 comparisons. In Big O notation, smaller terms drop out and constants are ignored, leaving a final Big O of O(n²).

# #### 19.3.2 Efficiency of Insertion Sort

Insertion sort is another simple, but inefficient, sorting algorithm. The algorithm’s first iteration takes the second element in the vector and, if it’s less than the first element, swaps it with the first element. The second iteration looks at the third element and inserts it into the correct position with respect to the first two elements, so all three elements are in order. At the i-th iteration of this algorithm, the first i elements in the original vector will be sorted.

Insertion sort iterates n − 1 times, inserting an element into the appropriate position in the elements sorted so far. For each iteration, determining where to insert the element can require comparing the element to each of the preceding elements—n − 1 comparisons