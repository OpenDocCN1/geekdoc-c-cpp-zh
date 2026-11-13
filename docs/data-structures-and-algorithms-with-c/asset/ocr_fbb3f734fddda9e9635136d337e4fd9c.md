```
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

# Time complexity of Shell Sort

Worst-case time complexity: The worst-case time complexity of the shell sort depends on the gap sequence (increment sequence). For the gap sequence 1, 4, 13, 40, 121,... the time complexity is O(n^1.32). It is easy for calculating the previous term of this gap sequence using integer arithmetic: GAP = GAP / 3

For the gap sequence 1, 2, 3, 4, 6, 8, 9, 12,... the time complexity is O(nlog^2 n). This is the best known performance compare to any other gap sequences, but it uses too many increments. Almost all the gap sequences gives the running time complexity O(n^1.32), some other gap sequences, time complexity is O(n^1.32).

Therefore, neither tight upper bounds on time complexity nor the best increment sequence are known.

| Shell Sort algorithm | Best Case | Average Case | Worst Case |
| :--- | :--- | :--- | :--- |
| | O(nlog^2 n) | O(nlog n) | O(n^1.32) |

Shell does is unstable and it has a higher cache miss ratio than quick sort. However, its low overhead (does not use the call stack), relatively simple implementation, adaptive properties, and sub-quadratic time complexity, shell-sort may be a feasible alternative to the O (nlogn) sorting algorithms for some applications when the data to be sorted is not very large.

# Time complexity of Sorting Algorithms

The following table covers the space complexity and time complexity in Big-O notation for different sorting algorithms commonly used in Computer Science.