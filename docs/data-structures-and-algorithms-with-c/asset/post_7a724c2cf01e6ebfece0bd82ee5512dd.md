
2. Repeat steps 3 to 5 while K < N
3. Set I = 0
4. Repeat while I <= N - K then
   a) If A[I] > A[I + 1] then
      Temp = A[I]
      A[I] = A[I + 1]
      A[I + 1] = Temp
   [End of If]
   b) Set I = I + 1
[End of Loop]
5. Set K = K + 1
[End of Loop]
6. Return

## Analysis / Time complexity of Bubble Sort

Best case / Worst case / Average case time complexity: In all the cases, the total number of comparisons:
f(n) = (n-1) + (n-2) + ... + 3 + 2 + 1 = \(\sum_{i=1}^{n-1} i = \frac{n(n-1)}{2} = O(n^2)\)

| Bubble Sort algorithm | Best Case | Average Case | Worst Case |
| :--- | :--- | :--- | :--- |
| | O(n²) | O(n²) | O(n²) |

## Refined Bubble Sort

Bubble sort may run in O(n) on sorting the data and works well on nearly sorted data. Refined bubble sort uses an extra Flag variable to indicate when no interchange takes place during a pass. When Flag = False after any pass, then the list is already sorted and there is no need to continue. This may cut down the number of passes. However, while using such Flag variable, one must initialize, reset and compare the variable during each pass.

## Algorithm of Refined Bubble Sort

```
Algorithm: BUBBLE_SORT (A, N)
[A is an array of N elements]
1. Set K = 1
2. Repeat steps 3 to 5 while K < N
3. Set I = 0, Flag = False
4. Repeat while I <= N - K then
   a) If A[I] > A[I + 1] then
      Temp = A[I]
      A[I] = A[I + 1]
      A[I + 1] = Temp
      Flag = True
   [End of If]
   b) Set I = I + 1
[End of Loop]
If Flag = False then Return
Set K = K + 1
[End of Loop]
Return
```

## Time complexity of Refined Bubble Sort

Best-case time complexity: The best case occurs when the array is already sorted. Total number of comparisons: f(n) = n - 1 = O(n)

Average-case / Worst-case time complexity: In both cases total number of comparisons:

```
f(n) = (n-1) + (n-2) + ... + 3 + 2 + 1 = \sum_{i=1}^{n-1} i = \frac{n(n-1)}{2} = O(n^2)
```

| Refined Bubble Sort algorithm | Best Case | Average Case | Worst Case |
|---|---|---|---|
| | O(n) | O(n²) | O(n²) |

Although popular, bubble sort has poor performance on random data. This observation is justified as shown in the following figure where bubble sort is nearly three times as slow as insertion sort.

![](img/723fa3ef35f5102eb67dc45b74bb823d_280_0.png)

Figure 10.5: Performance graph of Insertion, Selection and Bubble sort

## Insertion Sort

The intuitive idea is to insert a new element in the sorted array one by one (known as card player sort). As the insertion operation is performed in this sorting technique, hence it is named as insertion sort. This algorithm is known as on-line sorting algorithm as it can start even if not all the elements are present at the beginning.

Suppose A is an array with n elements from A[0] to A[N-1]. The insertion sort algorithm inserts each element A[K] into the sorted sub-array A[0], A[1], ..., A[K-1], so that after insertion the sub-array A[0], A[1], A[2], ..., A[K] remains sorted.

- The first array element A[0] by itself is trivially sorted.
- In the first pass, A[1] is inserted into its proper position so that, A[0], A[1] is sorted.
- In the second pass, A[2] is inserted into its proper position in A[0], A[1], so that, A[0], A[1], A[2] is sorted.
- In the third pass, A[3] is inserted into its proper position in A[0], A[1], A[2], so that, A[0], A[1], A[2], A[3] is sorted.
- In the N-1 pass, A[N-1] is inserted into its proper position in A[0], A[1], A[2], A[3], A[N-2], so that, A[0], A[1], A[2], ..., A[N-1] is sorted.

### Algorithm: Insertion Sort

```
Algorithm: INSERTION_SORT (A, N)
[A is an array of N elements]
1. Repeat steps 2 to 4 for K = 1 to N
2. Set Temp = A[K] and P = K - 1
3. Repeat while Temp < A[P] and P >= 0
   a) Set A[P + 1] = A[P]
   b) Set P = P - 1
   [End of loop]
4. Set A[P + 1] = Temp
   [End of loop]
5. Return
```

In this algorithm, two types of comparisons are required: one comparison checks for the element being searched for, and another comparison is required to check the search remains within the bounds of the list being searched. The number of comparisons can be reduced into one by using a so-called sentinel.

Generally, sentinels can be used in insertion sort algorithms to make them more efficient, effectively halving the number of comparisons in a loop. We can use the minimum element of the list as a sentinel. It takes three steps to sort the list:

- i) Find the minimum element of the list.
- ii) Interchange the minimum element with the 1st element of the list.
- iii) Finally, perform an efficient insertion sort on the list.

However, finding the minimum element of the list requires extra time. Alternatively, we can use a special value as a sentinel that requires extra memory space. Assume that the array of size n is actually stored from 1 to N positions and initialize A[0] with -∞. Here, -∞ is used as a sentinel element; in C language, it can be represented by INT_MIN. This ensures that whatever may be the value of Temp, always A[0] <= Temp.

Temp will be found among the locations 1, 2, ..., N, but never occupies the first position of the array.

The first two array elements A[0] and A[1] by themselves are trivially sorted.

## Example:

Input Data: 60, 80, 20, 50, 10, 15, 95 and 90

| Pass | A[0] | A[1] | A[2] | A[3] | A[4] | A[5] | A[6] | A[7] | A[8] |
|---|---|---|---|---|---|---|---|---|---|
| 1 | -∞ | 60 | 80 | 20 | 50 | 10 | 15 | 95 | 90 |
| 2 | -∞ | 60 | 80 | 20 | 50 | 10 | 15 | 95 | 90 |
| 3 | -∞ | 20 | 60 | 80 | 50 | 10 | 15 | 95 | 90 |
| 4 | -∞ | 20 | 50 | 60 | 80 | 10 | 15 | 95 | 90 |
| 5 | -∞ | 10 | 20 | 50 | 60 | 80 | 15 | 95 | 90 |
| 6 | -∞ | 10 | 15 | 20 | 50 | 60 | 80 | 95 | 90 |
| 7 | -∞ | 10 | 15 | 20 | 50 | 60 | 80 | 95 | 90 |
| Sorted List: | -∞ | 10 | 15 | 20 | 50 | 60 | 80 | 90 | 95 |

Figure 10.6: Insertion Sort

## Algorithm of Efficient Insertion Sort

```
Algorithm: INSERTION_SORT (A, N)
[A is an array of N elements]
1. Set A[0] = -∞
2. Repeat steps 3 to 5 for K = 2 to N
3. Set Temp = A[K] and P = K - 1
4. Repeat while Temp < A[P]
   a) Set A[P + 1] = A[P]
   b) Set P = P - 1
   [End of loop]
5. Set A[P + 1] = Temp
   [End of loop]
6. Return
```

## Time complexity of Insertion Sort

Best-case time complexity: The best case occurs when the array is already sorted. Thus, only one comparison is required in each pass, which is between the newly inserted elements with the last element of the sorted sub-list. In this case, total number of comparisons:
f(n) = 1 + 1 + 1 + ... + 1 = \sum_{i=1}^{n-1} 1 = n - 1 = O(n)

Worst-case time complexity: The worst case occurs when the array is in reverse order. Thus, we need to compare with all the elements of the sorted sub-list in each pass. In this case, total number of comparisons:
f(n) = 1 + 2 + 3 + ... + (n-1) = \sum_{i=1}^{n-1} i = \frac{n(n-1)}{2} = O(n^2)

Average-case time complexity: In the average case, on average, half of the elements of the sorted sub-list are less than the inserted element and half of the elements are greater. Thus, we need to compare half of the size of the sorted sub-list in each pass. In this case, total number of comparisons:
f(n) = \frac{1}{2} + \frac{2}{2} + \frac{3}{2} + ... + \frac{n-1}{2} = \sum_{i=1}^{n-1} \frac{i}{2} = \frac{n(n-1)}{4} = O(n^2)

| Insertion Sort algorithm | Best Case | Average Case | Worst Case |
|---|---|---|---|
| | O(n) | O(n^2) | O(n^2) |

## Selection Sort

In selection sorting algorithm, first select the smallest element in the list and place it in the first position. Then select the second smallest element in the list and place it in the second position, and so on. As selection operation is performed in this sorting technique, hence it is named as selection sort.

Suppose A is an array with N elements from A[0] to A[N-1]. The selection sorting algorithm selects the Kth smallest element A[K] from the array and places it into the K-1 position.

- In the pass 1, select the position POS of the smallest element in the list of N elements and then swapping A[POS] and A[0] so that, A[0] is sorted.
- In the pass 2, select the position POS of the smallest element in the sub-list of N-1 elements A[1], A[2], ...A[N-1] and then swapping A[POS] and A[1] so that, A[0], A[1] is sorted.
- In the pass 3, select the position POS of the smallest element in the sub-list of N-2 elements A[2], A[3],..., A[N-1] and then swapping A[POS] and A[2] so that, A[0], A[1], A[2] is sorted.
- In the pass N-1, select the position POS of the smallest element in the sub-list of 2 elements A[N-2], A[N-1] and then swapping A[POS] and A[N-2] so that, A[0], A[1], A[2],...,A[N-2] is sorted.
- The last array element A[N-1] is apparently the largest element of the array.

Therefore, array A of N elements from A[0] to A[N-1] is sorted after N-1 passes.

## Algorithm: Selection Sort

```
ALGORITHM: SELECTION_SORT (A, N)
[A is an array of N elements]
1. Repeat steps 2 and 3 for K = 1 to N - 1
2. Call MIN (A, K, N, LOC)
3. If A[K] != A[LOC] then
```
