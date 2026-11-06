# ## Outline

+   - **19.1** Introduction
+   - **19.2** Searching Algorithms
+     - 19.2.1 Efficiency of Linear Search
+     - 19.2.2 Binary Search
+   - **19.3** Sorting Algorithms
+     - **19.3.1** Efficiency of Selection Sort
+     - **19.3.2** Efficiency of Insertion Sort
+     - **19.3.3** Merge Sort (A Recursive Implementation)
+   - **19.4** Wrap-Up
+   
+   *Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

# ## 19.1 Introduction

Searching data involves determining whether a value (referred to as the search key) is present in the data and, if so, finding the value’s location. Two popular search algorithms are the simple linear search (introduced in Section 7.7) and the faster but more complex binary search, which is introduced in this chapter.

Sorting places data in order, typically ascending or descending, based on one or more sort keys. A list of names could be sorted alphabetically, bank accounts could be sorted by account number, employee payroll records could be sorted by social security number, and so on. Previously, you learned about insertion sort (Section 7.8) and selection sort (Section 8.6). This chapter introduces the more efficient, but more complex merge sort. Figure 19.1 summarizes the searching and sorting algorithms discussed in the examples and exercises of this book. This chapter also introduces Big O notation, which is used to estimate the worst-case runtime for an algorithm—that is, how hard an algorithm may have to work to solve a problem.

| Algorithm | Location |
|---|---|
| *Searching Algorithms* | |
| Linear search | Section 7.7 |
| Binary search | Section 19.2.2 |
| Recursive linear search | Exercise 19.8 |
| Recursive binary search | Exercise 19.9 |
| Binary tree search | Section 20.7 |
| Linear search of a linked list | Exercise 20.21 |
| `binary_search` standard library function | Section 22.5.6 |
| *Sorting Algorithms* | |
| Insertion sort | Section 7.8 |
| Selection sort | Section 8.6 |
| Recursive merge sort | Section 19.3.3 |
| Bubble sort | Exercises 19.5 and 19.6 |
| Bucket sort | Exercise 19.7 |
| Recursive quicksort | Exercise 19.10 |

**Fig. 19.1** | Searching and sorting algorithms in this text. (Part 1 of 2.)