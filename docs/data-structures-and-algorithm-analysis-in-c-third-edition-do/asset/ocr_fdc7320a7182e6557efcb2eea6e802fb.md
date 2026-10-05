234

Chap. 7 Internal Sorting

| i=1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---||
| 42 | 20 | 17 | 13 | 13 | 13 | 13 |
| 20 | 42 | 17 | 17 | 14 | 14 | 14 |
| 17 | 13 | 42 | 20 | 28 | 20 | 15 |
| 28 | 28 | 28 | 42 | 28 | 23 | 20 |
| 14 | 14 | 14 | 14 | 42 | 28 | 23 |
| 23 | 23 | 23 | 23 | 23 | | 48 |
| 15 | 15 | 15 | 15 | 15 | | 42 |

**Figure 7.1** An Illustration of Insertion Sort. Each column shows the array after the iteration with the indicated i in the outer **for** loop. Values after the line in each column have been inserted. Arrows indicate the upward motions of records through the array.

following is a C++ implementation. The input is an array of *n* records stored in array **A**.

```
template <typename T, typename Comp> // Insertion Sort
void insert(T A[], int n) {
  for (int i=1; i<n; i++) { // Insert i-th record
    for (int j=i; j>0 && Comp::prior(A[j], A[j-1])); j--)
      swap(A[j], A[j-1]);
  }
```

Consider the case where **insert** is processing the i-th record, which has key value **X**. The record is moved upward in the array as long as **X** is less than the key value immediately above it. As soon as a key value less or equal to **X** is encountered, the insertion is done with correct all records before it in the array have many swaps. Figure 7.1 illustrates how Insertion Sort works.

The **body** is made up of two nested **for** loops. The outer **for** loop is executed *n*-1 times. The inner **for** loop depends on how many keys in positions 1 to *i*-1 have a value less than that of the key in position i. In the worst case, each record must make its way to the top of the array. This would occur if the keys are initially arranged from highest to lowest, in the reverse of sorted order. In this case, the number of comparisons will be one the first time through the **for** loop, the second time, and so on.

$$\sum_{i=2}^{n} i^2/2 = \Theta(n^2)$$

In contrast, consider the best-case cost. This occurs when the keys begin in sorted order from lowest to highest. In this case, every pass through the inner **for** loop will fail immediately, and no values will be moved. The total number