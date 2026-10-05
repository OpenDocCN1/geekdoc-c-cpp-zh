236

Chap. 7 Internal Sorting

| i=0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|--|
| 42 | 13 | 13 | 13 | 13 | 13 | 13 |
| 20 | 42 | 14 | 14 | 14 | 14 | 14 |
| 17 | 20 | 42 | 15 | 15 | 15 | 15 |
| 28 | 14 | 17 | 20 | 20 | 23 | 23 |
| 23 | 15 | 17 | 20 | 42 | 23 | 28 |
| 15 | 23 | 23 | 28 | 28 | 28 | 42 |

**Figure 7.2** An illustration of Bubble Sort. Each column shows the values after the iteration with the indicated value of i in the outer *for* loop. Values in each column have been sorted. Arrows indicate the swaps that take place during a given iteration.

the two values are swapped. Once the smallest value is encountered, this process will cause it to “bubble” to the top of the array. The second pass through the array repeats this process. However, because we know that the smallest value reached of the array on the first pass, is less than the two elements on the second pass. Likewise, each succeeding pass through the array compares adjacent elements, looking at one less value than the preceding pass. Figure 7.2 illustrates Bubble Sort. C++ implementation is as follows:

```
template <typename E, typename Comp>
void bubbleSort(E A[], int n) { // Bubble up i'th largest
    for (int i=0; i<n-1; i++) {
        for (int j=n-1; j>i; j--) {
            if (Comp:prior(A[j], A[j-1]))
                swap(A[j], A[j-1]);
        }
    }
```

Bubble Sort’s number of comparisons is less. Regardless of the arrangement of values in the array, the number of comparisons made by the inner *for* loop is always i, leading to a total cost of

$$\sum_{i=1} i \approx n^2/2 = \Theta(n^2)$

Bubble Sort’s running time is roughly the same in the best, average, and worst is less than the immediately preceding it in the array. We can expect this to occur for about half the swaps in the average case, leading to $\Theta(n^2)$ for the expected number of swaps. The actual number of swaps performed by Bubble Sort will be identical to that performed by Insertion Sort.