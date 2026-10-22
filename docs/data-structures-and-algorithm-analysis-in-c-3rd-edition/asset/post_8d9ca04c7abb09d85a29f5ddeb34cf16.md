
> we easily see that
> 
> $$\lim_{n\to\infty} \frac{n^2}{2n \log n} = \infty$$
> because n grows faster than 2 log n. Thus, n^2 is in \Omega(2n log n).

This section presents the analysis for several simple code fragments.

## Example 3.9 We begin with an analysis of a simple assignment to an integer variable.

Because the assignment statement takes constant time, it is Θ(1).

```
a = b;
```

## Example 3.10 Consider a simple for loop.

```
sum = 0;
for (i=1; i<=n; i++)
sum += n;
```

The first line is Θ(1). The for loop is repeated n times. The third line takes constant time so, by simplifying rule (4) of Section 3.4.4, the total cost for executing the two lines making up the for loop is Θ(n). By rule (3), the cost of the entire code fragment is also Θ(n).

## Example 3.11 We now analyze a code fragment with several for loops, some of which are nested.

```
sum = 0;
for (i=1; i<=n; i++) // First for loop
for (j=1; j<=i; j++) // is a double loop
sum++;
for (k=0; k<n; k++) // Second for loop
A[k] = k;
```

This code fragment has three separate statements: the first assignment statement and the two for loops. Again the assignment statement takes constant time; call it c1. The second for loop is just like the one in Example 3.10 and takes c2n = Θ(n) time.

The first for loop is a double loop and requires a special technique. We work from the inside of the loop outward. The expression sum++ requires constant time; call it c3. Because the inner for loop is executed i times, by simplifying rule (4) it has cost c3i. The outer for loop is executed n times, but each time the cost of the inner loop is different because it costs c3i with i changing each time. You should see that for the first execution of the outer loop, i is 1. For the second execution of the outer loop, i is 2. Each time through the outer loop, i becomes one greater, until the last time through the loop when i = n. Thus, the total cost of the loop is c3 times the sum of the integers 1 through n. From Equation 2.1, we know that

∑_{i=1}^{n} i = n(n + 1)/2

which is Θ(n²). By simplifying rule (3), Θ(c1 + c2n + c3n²) is simply Θ(n²).

## Example 3.12 Compare the asymptotic analysis for the following two code fragments:

```
sum1 = 0;
for (i=1; i<=n; i++)      // First double loop
    for (j=1; j<=n; j++)    //   do n times
        sum1++;
```

```
sum2 = 0;
for (i=1; i<=n; i++)      // Second double loop
    for (j=1; j<=i; j++)    //   do i times
        sum2++;
```

In the first double loop, the inner for loop always executes n times. Because the outer loop executes n times, it should be obvious that the statement sum1++ is executed precisely n² times. The second loop is similar to the one analyzed in the previous example, with cost ∑_{j=1}^{n} j. This is approximately ½ n². Thus, both double loops cost Θ(n²), though the second requires about half the time of the first.

## Example 3.13 Not all doubly nested for loops are Θ(n²). The following pair of nested loops illustrates this fact.

```
sum1 = 0;
for (k=1; k<=n; k*=2)      // Do log n times
    for (j=1; j<=n; j++)    // Do n times
        sum1++;
```

```
sum2 = 0;
for (k=1; k<=n; k*=2)      // Do log n times
    for (j=1; j<=k; j++)    // Do k times
        sum2++;
```

![](img/7ea3c39173f146f675b63b146d1535f3_92_0.png)

Figure 3.4 An illustration of binary search on a sorted array of 16 positions. Consider a search for the position with value K = 45. Binary search first checks the value at position 7. Because 41 < K, the desired value cannot appear in any position below 7 in the array. Next, binary search checks the value at position 11. Because 56 > K, the desired value (if it exists) must be between positions 7 and 11. Position 9 is checked next. Again, its value is too great. The final search is at position 8, which contains the desired value. Thus, function binary returns position 8. Alternatively, if K were 44, then the same series of record accesses would be made. After checking position 8, binary would return a value of n, indicating that the search is unsuccessful.

The final example of algorithm analysis for this section will compare two algorithms for performing search in an array. Earlier, we determined that the running time for sequential search on an array where the search value K is equally likely to appear in any location is Θ(n) in both the average and worst cases. We would like to compare this running time to that required to perform a binary search on an array whose values are stored in order from lowest to highest.

Binary search begins by examining the value in the middle position of the array; call this position mid and the corresponding value k_mid. If k_mid = K, then processing can stop immediately. This is unlikely to be the case, however. Fortunately, knowing the middle value provides useful information that can help guide the search process. In particular, if k_mid > K, then you know that the value K cannot appear in the array at any position greater than mid. Thus, you can eliminate future search in the upper half of the array. Conversely, if k_mid < K, then you know that you can ignore all positions in the array less than mid. Either way, half of the positions are eliminated from further consideration. Binary search next looks at the middle position in that part of the array where value K may exist. The value at this position again allows us to eliminate half of the remaining positions from consideration. This process repeats until either the desired value is found, or there are no positions remaining in the array that might contain the value K. Figure 3.4 illustrates the binary search method. Figure 3.5 shows an implementation for binary search.

To find the cost of this algorithm in the worst case, we can model the running time as a recurrence and then find the closed-form solution. Each recursive call to binary cuts the size of the array approximately in half, so we can model the worst-case cost as follows, assuming for simplicity that n is a power of two.

T(n) = T(n/2) + 1 for n > 1;   T(1) = 1.

```
// Return the position of an element in sorted array "A" of
// size "n" with value "K".  If "K" is not in "A", return
// the value "n".
int binary(int A[], int n, int K) {
    int l = -1;
    int r = n;            // l and r are beyond array bounds
    while (l+1 != r) {  // Stop when l and r meet
        int i = (l+r)/2;  // Check middle of remaining subarray
        if (K < A[i]) r = i;      // In left half
        if (K == A[i]) return i; // Found it
        if (K > A[i]) l = i;      // In right half
    }
    return n; // Search value not in A
}
```

### Figure 3.5 Implementation for binary search.

If we expand the recurrence, we find that we can do so only log n times before we reach the base case, and each expansion adds one to the cost. Thus, the closed-form solution for the recurrence is T(n) = log n.

Function binary is designed to find the (single) occurrence of K and return its position. A special value is returned if K does not appear in the array. This algorithm can be modified to implement variations such as returning the position of the first occurrence of K in the array if multiple occurrences are allowed, and returning the position of the greatest value less than K when K is not in the array.

Comparing sequential search to binary search, we see that as n grows, the Θ(n) running time for sequential search in the average and worst cases quickly becomes much greater than the Θ(log n) running time for binary search. Taken in isolation, binary search appears to be much more efficient than sequential search. This is despite the fact that the constant factor for binary search is greater than that for sequential search, because the calculation for the next search position in binary search is more expensive than just incrementing the current position, as sequential search does.

Note however that the running time for sequential search will be roughly the same regardless of whether or not the array values are stored in order. In contrast, binary search requires that the array values be ordered from lowest to highest. Depending on the context in which binary search is to be used, this requirement for a sorted array could be detrimental to the running time of a complete program, because maintaining the values in sorted order requires to greater cost when inserting new elements into the array. This is an example of a tradeoff between the advantage of binary search during search and the disadvantage related to maintaining a sorted array. Only in the context of the complete problem to be solved can we know whether the advantage outweighs the disadvantage.
