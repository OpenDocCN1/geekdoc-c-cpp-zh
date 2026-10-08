results in two recursive calls to method SortArray with subarrays approximately half size of the original array, and a single call to method Merge. This call to Merge requires, at worst, $n-1$ comparisons to fill the original array, which is $O(n)$. (Recall that each element in the array can be chosen by comparing one element from each of the subarrays.) The two calls to method SortArray result in four recursive calls to SortArray, with each subarray roughly a quarter size of the original array, along with two calls to method Merge. These two calls require $n/2-1$ comparisons for a total number of comparisons $(n/2-1)+(n/2-1)=n-2$, which continues, until SortArray generating two additional calls to method SortArray and a Merge, until the algorithm splits the array into one-element subarrays. At each level, $O(n)$ comparisons are required to merge the subarrays. Each level splits the size of the arrays in half, so doubling the size of the array requires only one more level. Quadrupling the size of the array requires only two levels. This pattern is logarithmic with $\log n$ levels. This results in a total efficiency of $O(n \log n)$.

# Performance Tip 18.2

As you have noticed, the key to achieving the high efficiency of the merge sort is cleverly using additional memory. This is another example of the space/time trade-offif you have more space you can get your algorithm to run in less time and if you have less your algorithm may require more time. In industry, you might create apps for memory-constrained devices, which might prevent you from using the merge sort algorithm.

# 18.4 Summary of the Efficiency of Searching and Sorting Algorithms

Figure 18.7 summarizes the searching and sorting algorithms covered in this book and lists the Big O of each. Figure 18.8 lists the Big O expressions covered in this chapter, along with a number of values for $n$ to highlight the growth rates.

| Algorithm | Location | Big O |
|---|---|--|
| Searching Algorithms: | | |
| Linear Search | Section 18.2.1 | $O(n)$ |
| Binary Search | Section 18.2.2 | $O(\log n)$ |
| Recursive Linear Search | Exercise 18.8 | $O(n)$ |
| Recursive Binary Search | Exercise 18.9 | $O(\log n)$ |
| Sorting Algorithms: | | |
| Selection Sort | Section 18.3.1 | $O(n^2)$ |
| Insertion Sort | Section 18.3.2 | $O(n^2)$ |
| Merge Sort | Section 18.3.3 | $O(n \log n)$ |
| Bubble Sort | Exercises 18.5–18.6 | $O(n^2)$ |

**Fig. 18.7** | Searching and sorting algorithms with Big O values.

![](bbox=[0.14, 0.368, 0.213, 0.403])