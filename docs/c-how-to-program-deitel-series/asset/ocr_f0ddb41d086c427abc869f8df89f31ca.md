![](bbox=[0.0, 0.126, 0.095, 0.299])

+   - **20.1** Introduction
+   - **20.2** Searching Algorithms
+     - 20.2.1 Linear Search
+     - 20.2.2 Binary Search
+   - **20.3** Sorting Algorithms
+     - 20.3.1 Insertion Sort
+     - 20.3.2 Selection Sort
+     - 20.3.3 Merge Sort (A Recursive Implementation)
+   - **20.4** Wrap-Up
+   
+   *Summary* | *Self-Review Exercises* | *Answers to Self-Review Exercises* | *Exercises*

# 20.1 Introduction

**Searching** data involves determining whether a value (referred to as the **search key**) is present in the data and, if so, finding the value’s location. Two popular search algorithms are the simple **linear search** (Section 20.2.1) and the faster but more complex **binary search** (Section 20.2.2).

  **Sorting** places data in ascending or descending order, based on one or more **sort keys**. A list of names could be sorted alphabetically, bank accounts could be sorted by account number, employee payroll records could be sorted by social security number, and so on. You’ll learn about *insertion sort* (Section 20.3.1), *selection sort* (Section 20.3.2) and the more efficient, but more complex *merge sort* (Section 20.3.3). Figure 20.1 summarizes the searching and sorting algorithms discussed in the book’s examples and exercises. This chapter also introduces **Big O notation**, which is used to characterize an algorithm’s worst-case runtime—that is, how hard an algorithm may have to work to solve a problem.

| Algorithm | Location | Algorithm | Location |
|---|---|---|---|
| *Searching Algorithms* |  | *Sorting Algorithms* |  |
| Linear search | Section 20.2.1 | Insertion sort | Section 20.3.1 |
| Binary search | Section 20.2.2 | Selection sort | Section 20.3.2 |
| Recursive linear search | Exercise 20.8 | Recursive merge sort | Section 20.3.3 |
| Recursive binary search | Exercise 20.9 | Bubble sort | Exercises 20.5–20.6 |
| Binary tree search | Section 19.6 | Bucket sort | Exercise 20.7 |
| Linear search (linked list) | Exercise 19.21 | Recursive quicksort | Exercise 20.10 |
| binary search standard library function | Section 16.3.6 | Binary tree sort | Section 19.6 |
|  |  | sort standard library function | Section 16.3.6 |
|  |  | Heap sort | Section 16.3.12 |

**Fig. 20.1**  Searching and sorting algorithms in this text.

# *A Note About This Chapter’s Examples*

The searching and sorting algorithms in this chapter are implemented as function templates that manipulate objects of the array class template. To help you visualize how certain algorithms work, some of the examples display array-element values throughout the searching or sorting process. These output statements slow an algorithm’s performance and would *not* be included in industrial-strength code.