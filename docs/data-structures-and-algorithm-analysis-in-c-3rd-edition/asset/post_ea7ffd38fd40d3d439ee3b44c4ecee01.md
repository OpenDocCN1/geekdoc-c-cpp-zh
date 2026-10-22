
\[
\begin{aligned}
&= a^m T(1) + a^{m-1} c (n/b^{m-1})^k + \cdots + a c (n/b)^k + c n^k \\
&= a^m c + a^{m-1} c (n/b^{m-1})^k + \cdots + a c (n/b)^k + c n^k \\
&= c \sum_{i=0}^{m} a^{m-i} b^{ik} \\
&= c a^m \sum_{i=0}^{m} (b^k/a)^i.
\end{aligned}
\]

Note that

\[
a^m = a^{\log_b n} = n^{\log_b a}. \tag{14.1}
\]

The summation is a geometric series whose sum depends on the ratio \(r = b^k / a\). There are three cases.

1. **\(r < 1\).** From Equation 2.4, \(\sum_{i=0}^{m} r^i < 1/(1-r)\), a constant. Thus,
\[
T(n) = \Theta(a^m) = \Theta(n^{\log_b a}).
\]

2. **\(r = 1\).** Because \(r = b^k / a\), we know that \(a = b^k\). From the definition of logarithms it follows immediately that \(k = \log_b a\). We also note from Equation 14.1 that \(m = \log_b n\). Thus,
\[
\sum_{i=0}^{m} r^i = m + 1 = \log_b n + 1.
\]
Because \(a^m = n^{\log_b a} = n^k\), we have
\[
T(n) = \Theta(n^{\log_b a} \log n) = \Theta(n^k \log n).
\]

3. **\(r > 1\).** From Equation 2.5,
\[
\sum_{i=0}^{m} r^i = \frac{r^{m+1} - 1}{r - 1} = \Theta(r^m).
\]
Thus,
\[
T(n) = \Theta(a^m r^m) = \Theta(a^m (b^k / a)^m) = \Theta(b^{km}) = \Theta(n^k).
\]

We can summarize the above derivation as the following theorem, sometimes referred to as the Master Theorem.

### Theorem 14.1 (The Master Theorem)

For any recurrence relation of the form \(T(n) = a T(n/b) + c n^k\), \(T(1) = c\), the following relationships hold.

\[
T(n) =
\begin{cases}
\Theta(n^{\log_b a}) & \text{if } a > b^k, \\
\Theta(n^k \log n) & \text{if } a = b^k, \\
\Theta(n^k) & \text{if } a < b^k.
\end{cases}
\]

This theorem may be applied whenever appropriate, rather than re-deriving the solution for the recurrence.

### Example 14.10

Apply the Master Theorem to solve

\[
T(n) = 3 T(n/5) + 8 n^2.
\]

Because \(a = 3\), \(b = 5\), \(c = 8\), and \(k = 2\), we find that \(3 < 5^2\). Applying case (3) of the theorem, \(T(n) = \Theta(n^2)\).

### Example 14.11

Use the Master Theorem to solve the recurrence relation for Mergesort:

\[
T(n) = 2 T(n/2) + n; \quad T(1) = 1.
\]

Because \(a = 2\), \(b = 2\), \(c = 1\), and \(k = 1\), we find that \(2 = 2^1\). Applying case (2) of the theorem, \(T(n) = \Theta(n \log n)\).

### 14.2.4 Average-Case Analysis of Quicksort

In Section 7.5, we determined that the average-case analysis of Quicksort had the following recurrence:

\[
T(n) = c n + \frac{1}{n} \sum_{k=0}^{n-1} [T(k) + T(n-1-k)], \quad T(0) = T(1) = c.
\]

The \(c n\) term is an upper bound on the findpivot and partition steps. This equation comes from assuming that the partitioning element is equally likely to occur in any position \(k\). It can be simplified by observing that the two recurrence terms \(T(k)\) and \(T(n-1-k)\) are equivalent, because one simply counts up from \(T(0)\) to \(T(n-1)\) while the other counts down from \(T(n-1)\) to \(T(0)\). This yields

\[
T(n) = c n + \frac{2}{n} \sum_{k=0}^{n-1} T(k).
\]

This form is known as a recurrence with **full history**. The key to solving such a recurrence is to cancel out the summation terms. The shifting method for summations provides a way to do this. Multiply both sides by \(n\) and subtract the result from the formula for \((n+1)T(n+1)\):

\[
n T(n) = c n^2 + 2 \sum_{k=0}^{n-1} T(k)
\]

\[
(n+1)T(n+1) = c(n+1)^2 + 2 \sum_{k=0}^{n} T(k).
\]

Subtracting \(n T(n)\) from both sides yields:

\[
(n+1)T(n+1) - n T(n) = c(n+1)^2 - c n^2 + 2 T(n)
\]

\[
(n+1)T(n+1) - n T(n) = c(2n + 1) + 2 T(n)
\]

\[
(n+1)T(n+1) = c(2n + 1) + (n+2)T(n)
\]

\[
T(n+1) = \frac{c(2n+1)}{n+1} + \frac{n+2}{n+1} T(n).
\]

At this point, we have eliminated the summation and can now use our normal methods for solving recurrences to get a closed-form solution. Note that \(\frac{c(2n+1)}{n+1} < 2c\), so we can simplify the result. Expanding the recurrence, we get

\[
T(n+1) \le 2c + \frac{n+2}{n+1} T(n)
\]

\[
= 2c + \frac{n+2}{n+1} \left( 2c + \frac{n+1}{n} T(n-1) \right)
\]

\[
= 2c + \frac{n+2}{n+1} \left( 2c + \frac{n+1}{n} \left( 2c + \frac{n}{n-1} T(n-2) \right) \right)
\]

\[
= 2c + \frac{n+2}{n+1} \left( 2c + \cdots + \frac{4}{3} \left( 2c + \frac{3}{2} T(1) \right) \right)
\]

\[
= 2c \left( 1 + \frac{n+2}{n+1} + \frac{n+2}{n+1} \cdot \frac{n+1}{n} + \cdots + \frac{n+2}{n+1} \cdot \frac{n+1}{n} \cdots \frac{3}{2} \right)
\]

\[
= 2c \left( 1 + (n+2) \left( \frac{1}{n+1} + \frac{1}{n} + \cdots + \frac{1}{2} \right) \right)
\]

\[
= 2c + 2c(n+2)(\mathcal{H}_{n+1} - 1)
\]

for \(\mathcal{H}_{n+1}\), the Harmonic Series. From Equation 2.10, \(\mathcal{H}_{n+1} = \Theta(\log n)\), so the final solution is \(\Theta(n \log n)\).

## 14.3 Amortized Analysis

This section presents the concept of amortized analysis, which is the analysis for a series of operations taken as a whole. In particular, amortized analysis allows us to deal with the situation where the worst-case cost for \(n\) operations is less than \(n\) times the worst-case cost of any one operation. Rather than focusing on the individual cost of each operation independently and summing them, amortized analysis looks at the cost of the entire series and “charges” each individual operation with a share of the total cost.

We can apply the technique of amortized analysis in the case of a series of sequential searches in an unsorted array. For \(n\) random searches, the average-case cost for each search is \(n/2\), and so the expected total cost for the series is \(n^2/2\). Unfortunately, in the worst case all of the searches would be to the last item in the array. In this case, each search costs \(n\) for a total worst-case cost of \(n^2\). Compare this to the cost for a series of \(n\) searches such that each item in the array is searched for precisely once. In this situation, some of the searches must be expensive, but also some searches must be cheap. The total number of searches, in the best, average, and worst case, for this problem must be \(\sum_{i=1}^{n} i \approx n^2/2\). This is a factor of two better than the more pessimistic analysis that charges each operation in the series with its worst-case cost.

As another example of amortized analysis, consider the process of incrementing a binary counter. The algorithm is to move from the lower-order (rightmost) bit toward the high-order (leftmost) bit, changing 1s to 0s until the first 0 is encountered. This 0 is changed to a 1, and the increment operation is done. Below is C++ code to implement the increment operation, assuming that a binary number of length \(n\) is stored in array \(A\) of length \(n\).

```cpp
for (i=0; ((i<n) && (A[i] == 1)); i++)
    A[i] = 0;
if (i < n)
    A[i] = 1;
```

If we count from 0 through \(2^n - 1\) (requiring a counter with at least \(n\) bits), what is the average cost for an increment operation in terms of the number of bits processed? Naive worst-case analysis says that if all bits except the high-order bit are 1, then \(n\) bits need to be processed. Thus, if there are \(2^n\) increments, then the cost is \(n 2^n\). However, this is much too high, because it is rare for so many bits to be processed. In fact, half of the time the low-order bit is 0, and so only that bit is processed. One quarter of the time, the low-order two bits are 01, and so only the low-order two bits are processed. Another way to view this is that the low-order bit is always flipped, the bit to its left is flipped half the time, the next bit one quarter of the time, and so on. We can capture this with the summation

(charging costs to bits going from right to left)

\[
\sum_{i=0}^{n-1} \frac{1}{2^i} < 2.
\]

In other words, the average number of bits flipped on each increment is 2, leading to a total cost of only \(2 \cdot 2^n\) for a series of \(2^n\) increments.

A useful concept for amortized analysis is illustrated by a simple variation on the stack data structure, where the **pop** function is slightly modified to take a second parameter \(k\) indicating that \(k\) pop operations are to be performed. This revised pop function, called **multipop**, might look as follows:

```cpp
// pop k elements from stack
void multipop(int k);
```

The “local” worst-case analysis for **multipop** is \(\Theta(n)\) for \(n\) elements in the stack. Thus, if there are \(m_1\) calls to **push** and \(m_2\) calls to **multipop**, then the naive worst-case cost for the series of operations is \(m_1 + m_2 \cdot n = m_1 + m_2 \cdot m_1\). This analysis is unreasonably pessimistic. Clearly it is not really possible to pop \(m_1\) elements each time **multipop** is called. Analysis that focuses on single operations cannot deal with this global limit, and so we turn to amortized analysis to model the entire series of operations.

The key to an amortized analysis of this problem lies in the concept of **potential**. At any given time, a certain number of items may be on the stack. The cost for **multipop** can be no more than this number of items. Each call to **push** places another item on the stack, which can be removed by only a single **multipop** operation. Thus, each call to **push** raises the potential of the stack by one item. The sum of costs for all calls to **multipop** can never be more than the total potential of the stack (aside from a constant time cost associated with each call to **multipop** itself).

The amortized cost for any series of **push** and **multipop** operations is the sum of three costs. First, each of the **push** operations takes constant time. Second, each **multipop** operation takes a constant time in overhead, regardless of the number of items popped on that call. Finally, we count the sum of the potentials expended by all **multipop** operations, which is at most \(m_1\), the number of **push** operations. This total cost can therefore be expressed as

\[
m_1 + (m_2 + m_1) = \Theta(m_1 + m_2).
\]

A similar argument was used in our analysis for the partition function in the Quicksort algorithm (Section 7.5). While on any given pass through the while loop the left or right pointers might move all the way through the remainder of the
