
## Algorithm of Radix Sort

```
Algorithm: RADIX_SORT (A, N)
[Q is an array of Circular Queue of size 10]
[A is an array of N elements]
1. Initialize array Q
2. Set X = maximum element of A
3. Count the digits of X and Set pass = number of digits
4. Set DIV = 1
5. Repeat For I = 1 to pass do
6.     Repeat steps For J = 0 to N-1 do
7.         Set Remainder = A[J] mod (DIV * 10)
8.         Set Remainder = Remainder / DIV
9.         Call INSERT (Q[Remainder], A[J])
   [End of Loop]
10. Set DIV = DIV * 10
11. Delete the elements from the queue and place them into A
12. [End of Loop]
13. Return
```

## Time complexity of Radix Sort

The lower bound of the comparison-based sorting algorithms (Quick sort, Merge sort, Heap sort etc.) is Ω(nlog n), i.e. they cannot be better than nlog n to sort n keys.

Now, let there be k average digits in the input data for Radix sort, b is the base for representing numbers, for example, for the decimal system, b is 10. An LSD radix sort takes O(k*(n+b)) or O(nk) time. Sometimes k is presented as a constant, which would make the radix sort better (for sufficiently large n) than the best comparison-based sorting algorithms. The space complexity of the radix sort is O(n+b) as it needs space for the original numbers and b buckets to place the n items.

| Radix Sort algorithm | Best Case | Average Case | Worst Case |
|---|---|---|---|
| Radix Sort algorithm | O(nk) | O(nk) | O(nk) |

## Shell Sort

Shell sort can be seen as a generalized form of insertion sort. Donald Shell published the first version of this sort in 1959. As Donald Shell developed this sorting technique, hence it is named as Shell sort. The difficulty for insertion sort is that an element moves towards its final position very slowly, one position at a time and it cannot make a long jump quickly to reach its destination.

```
h number of independent sub-arrays {
A[0]   A[h]   A[2h]   A[3h]   ......
A[1]   A[h+1] A[2h+1] A[3h+1] ......
A[2]   A[h+2] A[2h+2] A[3h+2] ......
.      .      .       .
.      .      .       .
.      .      .       .
A[h-1] A[2h-1] A[3h-1] A[4h-1] ......
}
```

Figure 10.17: h independent sub-arrays

Sort the sub-array using insertion sorting technique. The difference between two consecutive elements of a sub-array is h. In general, an array is to be sorted for several values of h, which forms a monotone decreasing sequence and the last value of h sequence must be always one. The last pass is same as an ordinary insertion sort. More specifically, a sequence of numbers are

$h_1 > h_2 > ... > h_{t-2} > ... > h_2 > h_1 = 1$

to be decided and the array is to be sorted over t different passes using the method. The general idea in insertion sort, the predecessor of a[i] is always a[i-1], but in the shell sort predecessor of a[i] is a[i-h] for some value of h.

### Example:

Suppose A is an array with 12 elements from A[1] to A[12]. Array elements are: 60, 80, 20, 50, 10, 15, 95, 90, 45, 70, 25 and 30

| | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] | [10] | [11] | [12] |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Input Data | 60 | 80 | 20 | 50 | 10 | 15 | 95 | 90 | 45 | 70 | 25 | 30 |
| After 5-sorting | 15 | 30 | 20 | 45 | 10 | 25 | 80 | 90 | 50 | 70 | 60 | 95 |
| After 3-sorting | 15 | 10 | 20 | 45 | 30 | 25 | 70 | 60 | 50 | 80 | 90 | 95 |
| After 1-sorting | 10 | 15 | 20 | 25 | 30 | 45 | 50 | 60 | 70 | 80 | 90 | 95 |

Figure 10.18: Shell sort

- At the first pass, 5-sorting (h = 5) performs insertion sort on the separate sub-arrays (A[1], A[6], A[11]), (A[2], A[7], A[12]), (A[3], A[8]), (A[4], A[9]) and (A[5], A[10]).
- In the second pass, 3-sorting (h = 3) performs insertion sort on the separate sub-arrays (A[1], A[4], A[7], A[10]), (A[2], A[5], A[8], A[11]) and (A[3], A[6], A[9], A[12]).
- In the third and final pass, 1 sorting (h = 1), is an ordinary insertion sort of the entire array (A[1], A[2], ...A[12]).

## Algorithm of Shell Sort

```
Algorithm: SHELL_SORT (A, N)
[A is an array of N elements]
1. Set GAP = LAST_GAP_SEQUENCE
2. Repeat steps 3 to 8 while GAP >= 1
3. Set I = GAP
4. Repeat steps 5 to 7 For I = GAP to N - 1
5. Set Temp = A[I]
6. Repeat while J >= GAP and A[J-GAP] > Temp
   a) Set A[J] = A[J-GAP]
   b) Set J = J - GAP
[End of loop]
7. Set A[J+GAP] = Temp
[End of loop]
8. Set GAP = PREV_GAP
[End of Loop]
9. Return
```

There are different gap sequences; each of them gives correct sort. However, the properties of thus obtained versions of Shell sort may be different. Some of the gap sequences are given in the following table. These are increasing in infinite sequences, whose elements less than n should be used in reverse order.

| Gap Sequence | General Term (k>=1) | Worst-case time complexity |
| :--- | :--- | :--- |
| 1, 4, 13, 40, 121, ... | (3^k+1)/2 less than [n/3] | O(n^1.32) |
| 1, 3, 5, 9, 17, 33, ... | 2^k+1, prefixed with 1 | O(n^1.32) |
| 1, 3, 7, 15, 31, ... | 2^k-1 | O(n^1.32) |
| 1, 2, 3, 4, 6, 8, 9, 12... | 2^p3^q | O(nlog^2 n) |

## Time complexity of Shell Sort

Worst-case time complexity: The worst-case time complexity of the shell sort depends on the gap sequence (increment sequence). For the gap sequence 1, 4, 13, 40, 121,... the time complexity is O(n^1.32). It is easy for calculating the previous term of this gap sequence using integer arithmetic: GAP = GAP / 3

For the gap sequence 1, 2, 3, 4, 6, 8, 9, 12,... the time complexity is O(nlog^2 n). This is the best known performance compare to any other gap sequences, but it uses too many increments. Almost all the gap sequences gives the running time complexity O(n^1.32), some other gap sequences, time complexity is O(n^1.32).

Therefore, neither tight upper bounds on time complexity nor the best increment sequence are known.

| Shell Sort algorithm | Best Case | Average Case | Worst Case |
| :--- | :--- | :--- | :--- |
| | O(nlog^2 n) | O(nlog n) | O(n^1.32) |

Shell sort is unstable and it has a higher cache miss ratio than quick sort. However, its low overhead (does not use the call stack), relatively simple implementation, adaptive properties, and sub-quadratic time complexity, shell-sort may be a feasible alternative to the O(nlogn) sorting algorithms for some applications when the data to be sorted is not very large.

## Time complexity of Sorting Algorithms

The following table covers the space complexity and time complexity in Big-O notation for different sorting algorithms commonly used in Computer Science.

### Table 10.1: Space complexity and time complexity of different sorting algorithms

| Algorithm | Best Case | Average Case | Worst Case | Stable | Space Complexity Worst Case |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Refined Bubble Sort | O(n) | O(n²) | O(n²) | Yes | O(1) |
| Selection Sort | O(n²) | O(n²) | O(n²) | No | O(1) |
| Insertion Sort | O(n) | O(n²) | O(n²) | Yes | O(1) |
| Quick Sort | O(nlog n) | O(nlog n) | O(n²) | No | O(log n) |
| Merge Sort | O(nlog n) | O(nlog n) | O(nlog n) | Yes | O(n) |
| Heap Sort | O(nlog n) | O(nlog n) | O(nlog n) | No | O(1) |
| Shell Sort | O(n) | O(n^1.5) | O(nlog² n) | No | O(1) |
| Radix Sort | O(nk) | O(nk) | O(nk) | No | O(n+k) |
| Bucket Sort | O(n+k) | O(n+k) | O(n+k) | Yes | O(n+k) |

## Summary

- Linear or sequential search is the simplest searching technique.
- Binary search finding the position of a particular value within the sorted list.
- A sorting algorithm is said to be stable, if two elements that are equal remain in the same relative order even after performing sorting.
- A sorting algorithm is in-place only if a constant amount of data elements of an input array is never stored outside the array.
- The lower bound of the comparison-based sorting algorithms is Ω(nlog n).
- Bubble sort is a simplest sorting technique that compares each pair of adjacent items and interchanging them if they are in the reverse order.
- Quicksort and Mergesort algorithm are based on recursive divide-and-conquer technique.
- Radix sort is an example of non-comparison based sorting.

## Exercises

- 1. Write a Radix sort algorithm. Radix Sort the following list:
  189, 205, 986, 421, 97, 192, 535, 839, 562, 674
- 2. Describe Radix sort with an algorithm. Show that it works in linear time.
- 3. Write the insertion sort algorithm.
- 4. What do you mean by external sorting? How does it differ from internal sorting?
- 5. Write an algorithm for sorting a list of numbers in ascending order using selection sort technique.
- 6. Compare the complexity of insertion sort and selection sort. Find the time complexity of the quicksort algorithm.
- 7. Compare the time complexity between Quicksort and Bubble sort algorithm.
- 8. What is the advantage of binary search over linear search?
