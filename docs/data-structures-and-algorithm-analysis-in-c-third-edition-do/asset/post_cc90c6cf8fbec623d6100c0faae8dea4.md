
# 3.5 Calculating the Running Time for a Program

When analyzing these two code fragments, we will assume that $n$ is a power of two. The first code fragment has its outer **for** loop executed $n+1$ times because each iteration $k$ is multiplied by $2$ until it reaches $n$. Because the inner loop always executes $n$ times, the total cost for the first code fragment can be expressed as $\sum_{i=0}^{\log n} n$. Note that a variable substitution takes place to create the summation, with $k=2^i$. From Equation 2.3, the solution for this summation is $\Theta(n \log n)$. In the second code fragment, the outer loop is also executed $\log n+1$ times. The inner loop has cost $k$, which doubles each time. The summation can be expressed as $\sum_{i=0}^{\log n} 2^i$, which is assumed to be a power of two and again $k=2^i$. From Equation 2.2, we know that this summation is simply $\Theta(n)$.

What about other control statements? **While loops are analyzed in a manner similar to for**, the cost of an *if* statement in the worst case is the greater of the costs for the **then** and **else** clauses. This is also true for the average case, assuming that the size of $n$ does not affect the probability of executing one of the clauses (which is always, but not necessarily, true). For **switch** statements, the worst-case cost is that of the most expensive branch. For subroutine, simply adding the cost of the subroutine.

There are rare situations in which executing the various branches of an **if** or **switch** statement are functions of the input size. For example, input of size $n$, the **then** clause of an *if* statement might be executed with probability $1/n$. An example would be an *if* statement that executes the **then** clause only for the smallest of $n$. To perform an average-case analysis for the cost of the more expensive branch, the technique of amortized analysis (see Section 14.3) can come to rescue.

Determining the execution time of a recursive subroutine can be difficult. The running time for a recursive subroutine is typically expressed by a recurrence relation. For example, the recursive function **fact** of Section 2.5 calls itself with a value less than its input value. The result of this recursive call is multiplied by the input value, which takes constant time. Thus, the cost of the factorial function, if we wish to measure cost in terms of the number of multiplication operations, is one more than the number of multiplications made by the recursive call on the smaller input. Because the base case does no multiplications, its cost is zero. Thus, the running time for this function is expressed as

We know from Examples 2.8 and 2.13 that the closed-form solution for this recurrence relation is $\Theta(n)$.

74

Chap. 3 Algorithm Analysis

| Position | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Key | 11 | 13 | 21 | 26 | 29 | 36 | 40 | 41 | 45 | 51 | 54 | 65 | 65 | 72 | 77 | 83 |

**Figure 3.4** An illustration of binary search on a sorted array of 16 positions. Consider a search for the value $K=45$. Binary search first checks the value at 7. Because $41 < K$, the desired value does not appear in any position below 7. Next, binary search checks the value at 11. Because $56 > K$, the desired value (if it exists) must be between 7 and 11. Position 9 is checked next. Again, its value is too great. Thus, function **binary** search returns position 8. If $K$ were 44, then the same series of record accesses would be made. After checking position 8, **binary** would return a value of $n$, indicating that the search is unsuccessful.

The final example of algorithm analysis for this section will compare two algorithms for performing search in an array. Earlier, we determined that the running time for sequential search on an array where the search value $K$ is likely to appear in any location is $\Theta(n)$ in both the average and worst cases. We would like to compare this running time to that required to perform a **binary search** on an array whose values are stored in order from lowest to highest. Binary search begins by examining the value in the middle position of the array; call this mid and the corresponding value $k_{mid}$. If $k_{mid}=K$, this processing can stop immediately. This is unlikely to be the case. Furthermore, knowing the middle value provides useful information that can help guide the search process. In particular, if $k_{mid} > K$, then you know that the value $K$ cannot appear in any position greater than $mid$. Thus, you can eliminate future search in the upper half of the array. Conversely, if $k_{mid} < K$, then you know you can ignore all positions in the array less than $mid$. Either way, half of the positions are eliminated from further consideration. Binary search next looks at the middle position of the remaining array where value $K$ may exist. The value at this position again allows us to eliminate half of the remaining positions from consideration. This process repeats until either the desired value is found, or there are no positions remaining in the array that might contain the value $K$. Figure 3.4 illustrates the binary search method. Figure 3.5 shows an implementation for binary search. To find the cost in the worst case, we can model the time as follows, assuming for simplicity that $n$ is a power of two.

```
T(n) = T(n/2) + 1 for n > 1; T(1) = 1
```

93

# Sec. 3.5 Calculating the Running Time for a Program

```c
// Return the position of an element in sorted array
// size "n" with value "K". If "K" is not in "A",
// return n
int binary(int A[], int n, int K) {
    int l = -1;
    int r = n; // l and r beyond array bounds
    while (l+1 < r) { // Stop when l+1 and r meets
        int i = (l+r)/2; // Check middle of subarray
        if (K < A[i]) r = i; // In left half
        if (K == A[i]) return i; // Found it
        if (K > A[i]) l = i; // In right half
    }
    return n; // Search value not in A
}
```

Figure 3.5 Implementation for binary search

If we expand the recurrence, we find that we can do only n times before we reach the base case, and each expansion adds one to the cost. Thus, the closedform solution for recurrence is $T(n)=\log n$.
