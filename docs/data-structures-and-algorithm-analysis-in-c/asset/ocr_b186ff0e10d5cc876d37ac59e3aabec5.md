M₁ = (A₁,₂ - A₂,₂)(B₁,₁ + B₂,₂)
M₂ = (A₁,₁ + A₂,₂)(B₁,₁ + B₂,₂)
M₃ = (A₁,₁ - A₂,₁)(B₁,₁ + B₁,₂)
M₄ = (A₁,₁ + A₁,₂)B₂,₂
M₅ = A₁,₁(B₁,₂ - B₂,₂)
M₆ = A₂,₂(B₂,₁ - B₁,₁)
M₇ = (A₂,₁ + A₂,₂)B₁,₁

Once the multiplications are performed, the final answer can be obtained with eight more additions.

C₁,₁ = M₁ + M₂ - M₄ + M₆
C₁,₂ = M₄ + M₅
C₂,₁ = M₆ + M₇
C₂,₂ = M₂ - M₃ + M₅ - M₇

It is straightforward to verify that this tricky ordering produces the desired values. The running time now satisfies the recurrence

T(N) = 7T(N/2) + O(N²)

The solution of this recurrence is T(N) = O(N^(log₂ 7)) = O(N^2.81).

As usual, there are details to consider, such as the case when N is not a power of 2, but these are basically minor nuances. Strassen's algorithm is worse than the straightforward algorithm when N is fairly large. It does not generalize for the case where the matrices are sparse (contain many zero entries), and it does not easily parallelize. When run with floating-point entries, it is less stable numerically than the classic algorithm. Thus, until recently it had only limited applicability. Nevertheless, it has always represented an important theoretical milestone and certainly shows that in computer science, as in many other fields, even though a problem seems to have an intrinsic complexity, nothing is certain until proven.

# 10.3 Dynamic Programming

In the previous section, we saw that a problem that can be mathematically expressed recursively can also be expressed as a recursive algorithm, in many cases yielding a significant performance improvement over a more naive exhaustive search.

Any recursive mathematical formula could be directly translated to a recursive algorithm, but the underlying reality is that often the compiler will not do justice to the recursive algorithm, and an inefficient program results. When we suspect that this is likely to be the case, we must provide a little more help to the compiler, by rewriting the recursive algorithm as a nonrecursive algorithm that systematically records the answers to the subproblems in a table. One technique that makes use of this approach is known as dynamic programming.