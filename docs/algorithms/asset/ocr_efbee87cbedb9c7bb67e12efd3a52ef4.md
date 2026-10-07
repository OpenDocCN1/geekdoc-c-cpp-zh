146

5.4 Set cover

# Figure 5.11 (a) Eleven towns. (b) Towns that are within 30 miles of each other.

![](bbox=[0.085, 0.115, 0.715, 0.305])

is then, how many sets $S_k$ must be picked in order to cover all the towns in the county?

# Set Cover

Input: A set of elements $B$; $S_1, \dots, S_m \subseteq B$
Output: A selection of the $S_i$ whose union is $B$.
Cost: Number of sets picked.

(In our example, the elements of $B$ are the towns.) This problem lends itself immediately to a greedy solution:

Repeat until elements of $B$ are covered:

+   Pick the set $S_i$ with the largest number of uncovered elements.

It is extremely natural and intuitive. Let's see what it would do on our earlier example: It would first place a school at town $a$, since it covers the largest number of elements. Thereafter, it would choose three more schools—$c, j$, and either $f$ or $g$--for a total of four. The greedy scheme with just three schools, at $b, e$, and $i$, is optimal!

But luckily, it isn't far from optimal.

**Claim** Suppose $B$ contains $n$ elements and the optimal cover consists of $k$ sets. Then the greedy algorithm will use at most $k \ln n$ sets.$^2$

Let $n_t$ be the number of elements still uncovered after $t$ iterations of the greedy algorithm (so $n_0 = n$). Since these remaining elements are covered by the optimal

$^2$means "natural logarithm," that is, to the base $e$.