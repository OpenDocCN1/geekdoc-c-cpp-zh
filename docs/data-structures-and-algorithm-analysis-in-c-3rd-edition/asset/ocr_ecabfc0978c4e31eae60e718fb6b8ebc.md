T(2) = 1 ≤ 2². For the induction step, we need to show that T(n) ≤ n² implies that T(2n) ≤ (2n)² for n = 2^N, N ≥ 1. The induction hypothesis is

T(i) ≤ i², for all i ≤ n.

It follows that

T(2n) = 2T(n) + 2n ≤ 2n² + 2n ≤ 4n² ≤ (2n)²

which is what we wanted to prove. Thus, T(n) is in O(n²).

Is O(n²) a good estimate? In the next-to-last step we went from n²+2n to the much larger 4n². This suggests that O(n²) is a high estimate. If we guess something smaller, such as T(n) ≤ cn for some constant c, it should be clear that this cannot work because c2n = 2cn and there is no room for the extra n cost to join the two pieces together. Thus, the true cost must be somewhere between cn and n².

Let us now try T(n) ≤ n log n. For the base case, the definition of the recurrence sets T(2) = 1 ≤ (2·log 2) = 2. Assume (induction hypothesis) that T(n) ≤ n log n. Then,

T(2n) = 2T(n) + 2n ≤ 2n log n + 2n ≤ 2n(log n + 1) ≤ 2n log 2n

which is what we seek to prove. In similar fashion, we can prove that T(n) is in Ω(n log n). Thus, T(n) is also Θ(n log n).

# Example 14.6 We know that the factorial function grows exponentially. How does it compare to 2^n? To n^n? Do they all grow “equally fast” (in an asymptotic sense)? We can begin by looking at a few initial terms.

| n | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| n! | 1 | 2 | 6 | 24 | 120 | 720 | 5040 | 40320 | 362880 |
| 2^n | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 | 512 |
| n^n | 1 | 4 | 9 | 256 | 3125 | 46656 | 823543 | 16777216 | 387420489 |

We can also look at these functions in terms of their recurrences.

n! = { 1          n = 1
       n(n-1)!    n > 1 }

2^n = { 2          n = 1
        2(2^{n-1}) n > 1 }