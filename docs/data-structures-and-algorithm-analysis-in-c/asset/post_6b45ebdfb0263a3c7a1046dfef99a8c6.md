
/**
 * Cubic maximum contiguous subsequence sum algorithm.
 */
int maxSubSum( const vector< int > & a )
{
    int maxSum = 0;

    for( int i = 0; i < a.size( ); ++i )
        for( int j = i; j < a.size( ); ++j )
        {
            int thisSum = 0;

            for( int k = i; k < j; ++k )
                thisSum += a[ k ];

            if( thisSum > maxSum )
                maxSum = thisSum;
        }

    return maxSum;
}

### Figure 2.5 Algorithm 1

It turns out that a more precise analysis, taking into account the actual size of these loops, shows that the answer is \(\Theta(N^3)\) and that our estimate above was a factor of 6 too high (which is all right, because constants do not matter). This is generally true in these kinds of problems. The precise analysis is obtained from the sum \(\sum_{i=0}^{N-1} \sum_{j=i}^{N-1} \sum_{k=i}^{j} 1\), which tells how many times line 14 is executed. The sum can be evaluated inside out, using formulas from Section 1.2.3. In particular, we will use the formulas for the sum of the first N integers and first N squares. First we have

\(\sum_{k=i}^{j} 1 = j - i + 1\)

Next we evaluate

\(\sum_{j=i}^{N-1} (j - i + 1) = \frac{(N - i + 1)(N - i)}{2}\)

This sum is computed by observing that it is just the sum of the first \(N - i\) integers. To complete the calculation, we evaluate

\(\sum_{i=0}^{N-1} \frac{(N-i+1)(N-i-1)}{2} = \sum_{i=1}^{N} \frac{(N-i+1)(N-i+2)}{2}\)
\(= \frac{1}{2} \sum_{i=1}^{N} N^2 - \left(N + \frac{3}{2}\right) \sum_{i=1}^{N} i + \frac{1}{2} \sum_{i=1}^{N} (N^2 + 3N + 2) \sum_{i=1}^{N} 1\)
\(= \frac{1}{2} \frac{N(N+1)(2N+1)}{6} - \left(N + \frac{3}{2}\right) \frac{N(N+1)}{2} + \frac{N^2 + 3N + 2}{2} N\)
\(= \frac{N^2 + 3N + 2N}{6}\)

We can avoid the cubic running time by removing a for loop. This is not always possible, but in this case there are an awful lot of unnecessary computations present in the algorithm. The inefficiency that the improved algorithm corrects can be seen by noticing that \(\sum_{i=k}^{N} A_k = \sum_{i=1}^{N} A_k\), so the computation at lines 13 and 14 in algorithm 1 is unduly expensive. Figure 2.6 shows an improved algorithm. Algorithm 2 is clearly \(O(N^2)\); the analysis is even simpler than before.

/**
 * Quadratic maximum contiguous subsequence sum algorithm.
 */
int maxSubSum2( const vector<int> & a )
{
  int maxSum = 0;

  for( int i = 0; i < a.size( ); ++i )
  {
    int thisSum = 0;
    for( int j = i; j < a.size( ); ++j )
    {
      thisSum += a[ j ];

      if( thisSum > maxSum )
        maxSum = thisSum;
    }
  }

  return maxSum;
}

### Figure 2.6 Algorithm 2

which are then solved recursively. This is the “divide” part. The “conquer” stage consists of patching together the two solutions of the subproblems, and possibly doing a small amount of additional work, to arrive at a solution for the whole problem.

In our case, the maximum subsequence sum can be in one of three places. Either it occurs entirely in the left half of the input, or entirely in the right half, or it crosses the middle and is in both halves. The first two cases can be solved recursively. The last case can be obtained by finding the largest sum in the first half that includes the last element in the first half, and the largest sum in the second half that includes the first element in the second half. These two sums can then be added together. As an example, consider the following input:

| First Half | Second Half |
| :--- | :--- |
| 4 -3 5 -2 | -1 2 6 -2 |

The maximum subsequence sum for the first half is 6 (elements A1 through A3) and for the second half is 8 (elements A6 through A7).

The maximum sum in the first half that includes the last element in the first half is 4 (elements A1 through A4), and the maximum sum in the second half that includes the first element in the second half is 7 (elements A5 through A7). Thus, the maximum sum that spans both halves and goes through the middle is 4 + 7 = 11 (elements A1 through A7).

We see, then, that among the three ways to form a large maximum subsequence, for our example, the best way is to include elements from both halves. Thus, the answer is 11. Figure 2.7 shows an implementation of this strategy.

The code for algorithm 3 deserves some comment. The general form of the call for the recursive function is to pass the input array along with the left and right borders, which delimits the portion of the array that is operated upon. A one-line driver program sets this up by passing the borders 0 and N – 1 along with the array.

Lines 8 to 12 handle the base case. If left == right, there is one element, and it is the maximum subsequence if the element is nonnegative. The case left > right is not possible unless N is negative (although minor perturbations in the code could mess this up). Lines 15 and 16 perform the two recursive calls. We can see that the recursive calls are always on a smaller problem than the original, although minor perturbations in the code could destroy this property. Lines 18 to 24 and 26 to 32 calculate the two maximum sums that touch the center divider. The sum of these two values is the maximum sum that spans both halves. The routine max3 (not shown) returns the largest of the three possibilities.

Algorithm 3 clearly requires more effort to code than either of the two previous algorithms. However, shorter code does not always mean better code. As we have seen in the earlier table showing the running times of the algorithms, this algorithm is considerably faster than the other two for all but the smallest of input sizes.

The running time is analyzed in much the same way as for the program that computes the Fibonacci numbers. Let T(N) be the time it takes to solve a maximum subsequence sum problem of size N. If N = 1, then the program takes some constant amount of time to execute lines 8 to 12, which we shall call one unit. Thus, T(1) = 1. Otherwise, the

```
1 /**
2  * Recursive maximum contiguous subsequence sum algorithm.
3  * Finds maximum sum in subarray spanning a[left..right].
4  * Does not attempt to maintain actual best sequence.
5  *
6  * int maxSubRec( const vector<int>& a, int left, int right )
7  {
8  if( left == right )  // Base case
9  {
10  if( a[ left ] > 0 )
11  return a[ left ];
12  else
13  return 0;
14 }
15
16 int center = ( left + right ) / 2;
17 int maxLeftSum  = maxSubRec( a, left, center );
18 int maxRightSum = maxSubRec( a, center + 1, right );
19
20 int maxLeftBorderSum = 0, leftBorderSum = 0;
21 for( int i = center; i >= left; --i )
22 {
23  leftBorderSum += a[ i ];
24  if( leftBorderSum > maxLeftBorderSum )
25  maxLeftBorderSum = leftBorderSum;
26 }
27
28 int maxRightBorderSum = 0, rightBorderSum = 0;
29 for( int j = center + 1; j <= right; ++j )
30 {
31  rightBorderSum += a[ j ];
32  if( rightBorderSum > maxRightBorderSum )
33  maxRightBorderSum = rightBorderSum;
34 }
35
36 return max3( maxLeftSum, maxRightSum,
37  maxLeftBorderSum + maxRightBorderSum );
38 }
39
40 /**
41  * Driver for divide-and-conquer maximum contiguous
42  * subsequence sum algorithm.
43  */
44 int maxSubSum3( const vector<int>& a )
45 {
46  return maxSubRec( a, 0, a.size( ) - 1 );
47 }
```

### Figure 2.7 Algorithm 3

program must perform two recursive calls, the two for loops between lines 19 and 32, and some small amount of bookkeeping, such as lines 14 and 34. The two for loops combine to touch every element in the subarray, and there is constant work inside the loops, so the time expended in lines 19 to 32 is O(N). The code in lines 8 to 14, 18, 26, and 34 is all a constant amount of work and can thus be ignored compared with O(N). The remainder of the work is performed in lines 15 and 16. These lines solve two subsequence problems of size N/2 (assuming N is even). Thus, these lines take T(N/2) units of time each, for a total of 2T(N/2). The total time for the algorithm then is 2T(N/2) + O(N). This gives the equations

T(1) = 1
T(N) = 2T(N/2) + O(N)

To simplify the calculations, we can replace the O(N) term in the equation above with N, since T(N) will be expressed in Big-Oh notation anyway, this will not affect the answer. In Chapter 7, we shall see how to solve this equation rigorously. For now, if T(N) = 2T(N/2) + N, and T(1) = 1, then T(2) = 4 = 2 * 2, T(4) = 12 = 4 * 3, T(8) = 32 = 8 * 4, and T(16) = 80 = 16 * 5. The pattern that is evident, and can be derived, is that if N = 2^k, then T(N) = N * (k + 1) = N log N + N = O(N log N).

This analysis assumes N is even, since otherwise N/2 is not defined. By the recursive nature of the analysis, it is really valid only when N is a power of 2, since otherwise we eventually get a subproblem that is not an even size, and the equation is invalid. When N is not a power of 2, a somewhat more complicated analysis is required, but the Big-Oh result remains unchanged.

In future chapters, we will see several clever applications of recursion. Here, we present a fourth algorithm to find the maximum subsequence sum. This algorithm is simpler to implement than the recursive algorithm and also is more efficient. It is shown in Figure 2.8.

It should be clear why the time bound is correct, but it takes a little thought to see why the algorithm actually works. To sketch the logic, note that like algorithms 1 and 2, j is representing the end of the current sequence, while i is representing the start of the current sequence. It happens that the use of i can be optimized out of the program if we do not need to know where the actual best subsequence is, but in designing the algorithm, lets pretend that i is needed and that we are trying to improve algorithm 2. One observation is that if a[i] is negative, then it cannot possibly be the start of the optimal subsequence, since any subsequence that begins by including a[i] would be improved by beginning with a[i+1]. Similarly, any negative subsequence cannot possibly be a prefix of the optimal subsequence (same logic). If, in the inner loop, we detect that the subsequence from a[i] to a[j] is negative, then we can advance i. The crucial observation is that not only can we advance i to i + 1, but we can also actually advance i all the way to j + 1. To see this, let p be any index between i + 1 and j. Any subsequence that starts at index p is not longer than the corresponding subsequence that starts at index i and includes the subsequence from a[i] to a[p - 1], since the latter subsequence is not negative (j is the first index that causes the subsequence starting at index i to become negative). Thus, advancing i to j + 1 is risk free; we cannot miss an optimal solution.

This algorithm is typical of many clever algorithms: The running time is obvious, but the correctness is not. For these algorithms, formal correctness proofs (more formal
