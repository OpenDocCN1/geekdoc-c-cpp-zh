
The answer is the highest value of LIS(k) for all k in range [0 ... N-1].

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| X | -7 | 10 | 9 | 2 | 3 | 8 | 8 | 1 |
| LIS(i) | 1 | 2 | 2 | 2 | 3 | 4 | 4 | 2 |

Figure 3.9: Longest Increasing Subsequence

In Figure 3.9, we see that:

LIS(0) is 1, the number -7 itself.

LIS(1) is now 2, as we can form {-7, 10} of length 2.

LIS(2) is also 2, as we can form {-7, 9}, but not {-7, 10} + {9} as it is non-increasing.

LIS(3) is also 2, we can only form {-7, 2}. {-7, 10} + {2} or {-7, 9} + {2} are both non-increasing.

LIS(4) is now 3, as we can extend {-7, 2} + {3} and this is the longest among other forms.

And so on until LIS(7). The answers are in LIS(5) or LIS(6), both with length 4.

There are clearly many overlapping sub-problems in LIS problem, but there are only N states, i.e. the LIS ending at index i, for all i ∈ [0 ... N-1]. As we need to compute each state with an O(n) loop, then this DP algorithm runs in O(n^2). The LIS solution(s) can be reconstructed by following the arrows via some backtracking routine (scrutinize the arrows in Figure 3.9 for LIS(5) or LIS(6)).

## Coin Change (CC) - The General Version

Problem^6: Given a target amount V cents and a list of denominations of N coins, i.e. We have coinValue[i] (in cents) for coin type i ∈ [0 ... N-1], what is the minimum number of coins that we must use to obtain amount V? Assume that we have unlimited supply of coins of any type.

Example 1:

V = 10, N = 2, coinValue = {1, 5}

We can use:

- A. Ten 1 cent coins = 10 x 1 = 10; Total coins used = 10
- B. One 5 cents coin + Five 1 cent coins = 1 x 5 + 5 x 1 = 10; Total coins used = 6
- C. Two 5 cents coins = 2 x 5 = 10; Total coins used = 2 -> Optimal

Recall that we can use greedy solution if the coin denominations are suitable - as in Example 1 above (See Section 3.3). But for general cases, we have to use DP - as in Example 2 below:

Example 2:

V = 7, N = 4, coinValue = {1, 3, 4, 5}

Greedy solution will answer 3, using 5+1+1 = 7, but optimal solution is 2, using 4+3 only!

Solution: Use these Complete Search recurrences:

- 1. coin(0) = 0 // 0 coin to produce 0 cent
- 2. coin(< 0) = INVALID -> (in practice, we just return a large positive value)
- 3. coin(value) = 1 + min(coin(value - coinValue[i])) ∀i ∈ [0..N-1]

The answer is in coin(V).

⁶There are other variants of this problem, e.g. counting how many ways to do coin change and a variant where supply of coins are limited.

| <0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| ∞ | 0 | 1 | 2 | 3 | 4 | 1 | 2 | 3 | 4 | 5 | 2 |

$V = 10$, $N = 2$,  
coinValue = {1, 5}

Both bottom up and top down DP happen to produce the same table...

Figure 3.10: Coin Change

In Figure 3.10, we see that:

coin(0) = 0, base case one.

coin(< 0) = ∞, base case two.

coin(1) = 1, from 1 + coin(1−1), as 1 + coin(1−5) is infeasible.

coin(2) = 2, from 1 + coin(2−1), as 1 + coin(2−5) is also infeasible.

... same thing for coin(3) and coin(4).

coin(5) = 1, from 1 + coin(5−5) = 1 coin, smaller than 1 + coin(5−1) = 5 coins.

And so on until coin(10). The answer is in coin(10), which is 2.

We can see that there are a lot of overlapping sub-problems in this Coin Change problem, but there are only $O(V)$ possible states! As we need to try $O(N)$ coins per state, the overall time complexity of this DP solution is $O(VN)$.

## Maximum Sum

Abridged problem statement: Given an n x n (1 ≤ n ≤ 100) array of integers, each ranging from [-127, 127], find a minimum sub-rectangle that has the maximum value.

Example: The 4 x 4 array (n = 4) below has 15 as the maximum sub-rectangle value.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_58_0.png)

Naïvely attacking this problem as shown below does not work as it is an $100^6$ algorithm.

```cpp
maxSubRect = -127*100*100; // lowest possible value for this problem
for (int i = 0; i < n; i++) for (int j = 0; j < n; j++) // start coord
  for (int k = i; k < n; k++) for (int l = j; l < n; l++) { // end coord
    subRect = 0; // sum items in this sub-rectangle
    for (int a = i; a <= k; a++) for (int b = j; b <= l; b++)
      subRect += arr[a][b];
    maxSubRect = max(maxSubRect, subRect); // keep largest so far
  }
```

Solution: There are several (well-known) DP solutions for static range problem. DP can work in this problem as computing a large sub-rectangle will definitely involves computing smaller sub-rectangles in it and such computation involves overlapping sub-rectangles!

One possible DP solution is to turn this n x n array into an n x n sum array where arr[i][j] no longer counts its own value, but the sum of all items within sub-rectangle (0, 0) to (i, j). This can easily be done on-the-fly when reading the input and still $O(n^2)$.

```cpp
scanf("%d", &n);
for (int i = 0; i < n; i++) for (int j = 0; j < n; j++) {
    scanf("%d", &arr[i][j]);
    if (i > 0) arr[i][j] += arr[i - 1][j]; // if possible, add values from top
    if (j > 0) arr[i][j] += arr[i][j - 1]; // if possible, add values from left
    if (i > 0 && j > 0) arr[i][j] -= arr[i - 1][j - 1]; // to avoid double count
} // inclusion-exclusion principle
```

This code turns input array (shown in the left) into sum array (shown in the right):

```text
0  -2  -7   0    ==>    0  -2  -9  -9
9   2  -6   2    ==>    9   9  -4   2
-4  1  -4   1    ==>    5   6 -11  -8
-1  8   0  -2    ==>    4  13  -4  -3
```

Now, with this sum array, we can answer the sum of any sub-rectangle (i, j) to (k, l) in $O(1)$! Suppose we want to know the sum of (1, 2) to (3, 3). We can split the sum array into 4 sections and compute

`arr[3][3] - arr[0][3] - arr[3][1] + arr[0][1] = -3 - 13 - (-9) + (-2) = -9.`

```text
0 [-2] | -9 [-9]
----------------
9   9  | -4   2
5   6  | -11 -8
4 [13]  -4 [-3]
```

With this $O(1)$ DP formulation, this problem can now be solved in $100^4$.

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

Lesson: Not every range problems require Segment Tree as in Section 2.3.3! Problems where the input data is static like this usually is solvable with DP technique.

- Exercise 1: The solution above runs in $100^4$. There exist $100^3$ solution. Can you figure out how to formulate this solution?
- Exercise 2: What if the given static array is 1-D? Can you form a similar $O(1)$ DP solution to answer range sum query(i, j), i.e. `arr[i] + arr[i+1] + ... + arr[j]`?
- Exercise 3: Use the solution from Exercise 2 to find maximum sum in 1-D array in $O(n^2)$. Can you further improve the solution to $O(n)$?
- Exercise 4: Now, what if the query is range minimum query(i, j) on 1-D static array. The solution in Section 2.3.3 uses Segment Tree. Can you just utilize DP to solve the same problem -- assuming that this time there is no update operation?

## Remarks

There are other classical DP problems that we choose not to cover in this book such as Matrix Chain Multiplication [4], Optimal Binary Search Tree [14], 0-1 Knapsack [5, 14]. However, Floyd Warshall's will be discussed in Section 4.7; String Edit Distance, Longest Common Subsequence (LCS), plus other DP on Strings in Section 6.3.

### 3.4.3 Non Classical Examples

Although DP is one problem type that is most frequently appears in recent programming contests, the classical DP problems on their *pure forms* above usually never appear again in recent ICPCs or IOIs. We have to study them to understand more about DP. But once we do, we have to move on to solve many other non classical DP problems and build up our ‘DP technique skills’. As you can see below, there are many interesting DP techniques from simple to intermediate. Try solving these problems at the corresponding online judges to further improve your DP skills. We have grouped and ordered the following DP problems from *our* perceived level of difficulty (easier to harder). There are DP trick lessons in each example. Enjoy :).

### 1. Cutting Sticks (UVa 10003)

Abridged problem statement: Given a stick of length 1 ≤ l ≤ 1000, make 1 ≤ n ≤ 50 cuts to that stick (coordinates within range (0 … l) are given). The cost of cut is determined by the length of the stick to be cut. Find a cutting sequence so that the overall cost is minimized!

Example: l = 100, n = 3, and cut coordinates: coord = {25, 50, 75} (already sorted)

If we cut from left to right, then we will incur cost = 225

- 1. Cut at coordinate 25, total cost = 100;
- 2. Cut at coordinate 50, total cost = 100 + 75 = 175;
- 3. Cut at coordinate 75, total cost = 175 + 50 = 225;

However, the optimal answer is: 200

- 1. Cut at coordinate 50, total cost = 100;
- 2. Cut at coordinate 25, total cost = 100 + 50 = 150;
- 3. Cut at coordinate 75, total cost = 150 + 50 = 200;

Solution: Use this Complete Search recurrences + top-down DP (memoization): cut(left, right)

- 1. If (left + 1 = right) where left and right are indices in array coord, then cut(left, right) = 0 as we are left with 1 segment, there is no need to cut anymore.
- 2. Otherwise, try all possible cutting points and pick the minimum cost using code below:

```cpp
// cost = initially infinity (a very large integer)
for (int i = left + 1; i < right; i++) // max 50 steps
    cost = min(cost, cut(left, i) + cut(i, right) + (coord[right] - coord[left]));
// after the loop above is done, we know that cut(left, right) = cost
```

Lesson: The Complete Search recurrences above only has 50×50 possible left/right indices configuration (states) and runs in just 50 × 50 × 50 = 125K operations! It is easy to convert this Complete Search / recursive backtracking recurrence into a top-down DP a.k.a memoization technique!
