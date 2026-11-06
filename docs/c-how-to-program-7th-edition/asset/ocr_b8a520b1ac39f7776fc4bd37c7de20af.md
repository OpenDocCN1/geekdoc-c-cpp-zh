```
    split:
                            26 54
                            26
                            54
    merge:
                            26
                            54
                            26 54
    merge:
                        18 60 78
                        26 54
                        18 26 54 60 78
    merge:
                22 30 47 67 79
                18 26 54 60 78
                18 22 26 30 47 54 60 67 78 79
    Sorted vector:
        18 22 26 30 47 54 60 67 78 79
```

Fig. 19.7 | MergeSort test program. (Part 3 of 3.)

Figure 19.8 summarizes the searching and sorting algorithms we cover in this book and lists the Big O for each. Figure 19.9 lists the Big O categories we’ve covered in this chapter along with a number of values for n to highlight the differences in the growth rates.

| Algorithm | Location | Big O |
|---|---|---|
| *Searching Algorithms* | | |
| Linear search | Section 7.7 | O(n) |
| Binary search | Section 19.2.2 | O(log n) |
| Recursive linear search | Exercise 19.8 | O(n) |
| Recursive binary search | Exercise 19.9 | O(log n) |
| *Sorting Algorithms* | | |
| Insertion sort | Section 7.8 | O(n²) |
| Selection sort | Section 8.6 | O(n²) |
| Merge sort | Section 19.3.3 | O(n log n) |
| Bubble sort | Exercises 19.5 and 19.6 | O(n²) |
| Quicksort | Exercise 19.10 | Worst case: O(n²)<br>Average case: O(n log n) |

Fig. 19.8 | Searching and sorting algorithms with Big O values.

| *n* | Approximate decimal value | *O(log n)* | *O(n)* | *O(n log n)* | *O(n²)* |
|---|---|---|---|---|---|
| 2^10 | 1000 | 10 | 2^10 | 10 · 2^10 | 2^20 |
| 2^20 | 1,000,000 | 20 | 2^20 | 20 · 2^20 | 2^40 |
| 2^30 | 1,000,000,000 | 30 | 2^30 | 30 · 2^30 | 2^60 |

Fig. 19.9 | Approximate number of comparisons for common Big O notations.