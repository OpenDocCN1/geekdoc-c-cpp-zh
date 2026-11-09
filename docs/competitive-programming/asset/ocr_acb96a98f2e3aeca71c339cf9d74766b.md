```
```cpp
scanf("%d", &n);
for (int i = 0; i < n; i++) for (int j = 0; j < n; j++) {
    scanf("%d", &arr[i][j]);
    if (i > 0) arr[i][j] += arr[i - 1][j]; // if possible, add values from top
    if (j > 0) arr[i][j] += arr[i][j - 1]; // if possible, add values from left
    if (i > 0 && j > 0) arr[i][j] -= arr[i - 1][j - 1]; // to avoid double count
} // inclusion-exclusion principle
```
```

This code turns input array (shown in the left) into sum array (shown in the right):

```
```text
0  -2  -7   0    ==>    0  -2  -9  -9
9   2  -6   2    ==>    9   9  -4   2
-4  1  -4   1    ==>    5   6 -11  -8
-1  8   0  -2    ==>    4  13  -4  -3
```
```

Now, with this sum array, we can answer the sum of any sub-rectangle (i, j) to (k, l) in $O(1)$! Suppose we want to know the sum of (1, 2) to (3, 3). We can split the sum array into 4 sections and compute

`arr[3][3] - arr[0][3] - arr[3][1] + arr[0][1] = -3 - 13 - (-9) + (-2) = -9.`

```
```text
0 [-2] | -9 [-9]
----------------
9   9  | -4   2
5   6  | -11 -8
4 [13]  -4 [-3]
```
```

With this $O(1)$ DP formulation, this problem can now be solved in $100^4$.

```
```cpp
maxSubRect = -127*100*100; // lowest possible value for this problem
for (int i = 0; i < n; i++) for (int j = 0; j < n; j++) // start coord
    for (int k = i; k < n; k++) for (int l = j; l < n; l++) { // end coord
        subRect = arr[k][l]; // this is sum of all items from (0, 0) to (k, l): O(1)
        if (i > 0) subRect -= arr[i - 1][l]; // O(1)
        if (j > 0) subRect -= arr[k][j - 1]; // O(1)
        if (i > 0 && j > 0) subRect += arr[i - 1][j - 1]; // inclusion-exclusion: O(1)
        maxSubRect = max(maxSubRect, subRect);
    }
```
```

Lesson: Not every range problems require Segment Tree as in Section 2.3.3! Problems where the input data is static like this usually is solvable with DP technique.

Exercise 1: The solution above runs in $100^4$. There exist $100^3$ solution. Can you figure out how to formulate this solution?

Exercise 2: What if the given static array is 1-D? Can you form a similar $O(1)$ DP solution to answer range sum query(i, j), i.e. `arr[i] + arr[i+1] + ... + arr[j]`?

Exercise 3: Use the solution from Exercise 2 to find maximum sum in 1-D array in $O(n^2)$. Can you further improve the solution to $O(n)$?

Exercise 4: Now, what if the query is range minimum query(i, j) on 1-D static array. The solution in Section 2.3.3 uses Segment Tree. Can you just utilize DP to solve the same problem -- assuming that this time there is no update operation?