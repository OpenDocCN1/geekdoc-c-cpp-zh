
## 3.3 Greedy

An algorithm is said to be greedy if it makes locally optimal choice at each step with the hope of finding the optimal solution. For some cases, greedy works - the solution code becomes short and runs efficiently. But for *many* others, it does not. As discussed in [4], a problem must exhibit two things in order for a greedy algorithm to work for it:

- 1. It has optimal sub-structures.
  
  Optimal solution to the problem contains optimal solutions to the sub-problems.

- 2. It has a greedy property (remark: hard to prove its correctness!).
  
  If we make a choice that seems best at the moment and solve the remaining subproblems later, we still reach optimal solution. We never have to reconsider our previous choices.

### 3.3.1 Classical Example

Suppose we have a large number of coins with different denominations, i.e. 25, 10, 5, and 1 cents. We want to make change with the *least number* of coins used. The following greedy algorithm works for this set of denominations of this problem: Keep using the largest denomination of coin which is not greater than the remaining amount to be made. Example: if the denominations are {25, 10, 5, 1} cents and we want to make a change of 42 cents, we can do: 42-25 = 17 → 17-10 = 7 → 7-5 = 2 → 2-1 = 1 → 1-1 = 0, of total 5 coins. This is optimal.

The coin changing example above has the two ingredients for a successful greedy algorithm:

- 1. It has optimal sub-structures.
  
  We have seen that in the original problem to make 42 cents, we have to use 25+10+5+1+1. This is an optimal 5 coins solution to the original problem!
  
  Now, the optimal solutions to its sub-problems are contained in this 5 coins solution, i.e.
  - a. To make 17 cents, we have to use 10+5+1+1 (4 coins),
  - b. To make 7 cents, we have to use 5+1+1 (3 coins), etc

- 2. It has a greedy property.
  
  Given every amount *V*, we greedily subtract it with the largest denomination of coin which is not greater than this amount *V*. It can be proven (not shown here for brevity) that using other strategy than this will not lead to optimal solution.

However, this greedy algorithm does *not* work for *all* sets of coin denominations, e.g. {1, 3, 4} cents. To make 6 cents with that set, a greedy algorithm would choose 3 coins {4, 1, 1} instead of the optimal solution using 2 coins {3, 3}. This problem is revisited later in Section 3.4.2.

There are many other classical examples of greedy algorithms in algorithm textbooks, for example: Kruskal’s for Minimum Spanning Tree (MST) problem – Section 4.4, Dijkstra’s for Single-Source Shortest Paths (SSSP) problem – Section 4.5, Greedy Activity Selection Problem [4], Huffman Codes [4], etc.

### 3.3.2 Non Classical Example

Today’s contest problems usually do not ask for solution of trivial and classical greedy problems. Instead, we are presented with novel ones that requires creativity, like the one shown below.

### UVa 410 - Station Balance

Given \(1 \le C \le 5\) chambers which can store 0, 1, or 2 specimens, \(1 \le S \le 2C\) specimens, and \(M\): a list of mass of the \(S\) specimens, determine in which chamber we should store each specimen in order to minimize IMBALANCE. See Figure 3.3 for visual explanation.

\(A = (\sum_{j=1}^{S} M_j)/C\), i.e. \(A\) is the average of all mass over \(C\) chambers.

\(\mathrm{IMBALANCE} = \sum_{i=1}^{C} |X_i - A|\), i.e. sum of differences between the mass in each chamber w.r.t \(A\).

where \(X_i\) is the total mass of specimens in chamber \(i\).

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_47_0.png)

Figure 3.3: Visualization of UVa 410 - Station Balance

This problem can be solved using a greedy algorithm. But first, we have to make several observations. If there exists an empty chamber, at least one chamber with 2 specimens must be moved to this empty chamber! Otherwise the empty chambers contribute too much to IMBALANCE! See Figure 3.4.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_47_1.png)

Figure 3.4: UVa 410 - Observation 1

Next observation: If \(S > C\), then \(S-C\) specimens must be paired with one other specimen already in some chambers. The Pigeonhole principle! See Figure 3.5.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_47_2.png)

Figure 3.5: UVa 410 - Observation 2

Now, the key insight that can simplify the problem is this: If \(S < 2C\), add dummy \(2C-S\) specimens with mass 0. For example, \(C = 3, S = 4, M = \{5, 1, 2, 7\} \Rightarrow C = 3, S = 6, M = \{5, 1, 2, 7, 0, 0\}\). Then, sort these specimens based on their mass such that \(M_1 \le M_2 \le \ldots \le M_{2C-1} \le M_{2C}\). In this example, \(M = \{5, 1, 2, 7, 0, 0\} \rightarrow \{0, 0, 1, 2, 5, 7\}\). By adding dummy specimens and then sorting them, a greedy strategy ‘appears’. We can now:
Pair the specimens with masses $M_1$ & $M_{2C}$ and put them in chamber 1, then pair the specimens with masses $M_2$ & $M_{2C-1}$ and put them in chamber 2, and so on . . .
This greedy algorithm — known as ‘Load Balancing’ — works! See Figure 3.6.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_48_0.png)

Figure 3.6: UVa 410 - Greedy Solution

To come up with this way of, as it is lightweight, but tends to get WA response. Proving that a certain problem has optimal sub-structure and greedy property in contest time may be time consuming, so a competitive programmer usually do this:

He will look at the input size. If it is ‘small enough’ for the time complexity of either Complete Search or Dynamic Programming (see Section 3.4), he will use one of these approaches as both will ensure correct answer. He will only use Greedy solution if he knows for sure that the input size given in the problem is too large for his best Complete Search or DP solution.

Having said that, it is quite true that many problem setters nowadays set the input size of such can-use-greedy-algorithm-or-not-problems to be in some reasonable range so contestants cannot use the input size to quickly determine the required algorithm!

Programming Exercises solvable using Greedy (hints omitted):

- 1. UVa 410 - Station Balance (elaborated in this section)
- 2. UVa 10020 - Minimal Coverage
- 3. UVa 10340 - All in All
- 4. UVa 10440 - Ferry Loading II
- 5. UVa 10670 - Work Reduction
- 6. UVa 10763 - Foreign Exchange
- 7. UVa 11054 - Wine Trading in Gergovia
- 8. UVa 11292 - Dragon of Loowater
- 9. UVa 11369 - Shopaholic

In this section, we want to highlight another problem solving trick called: *Decomposition!*

While there are only *few* basic algorithms used in contest problems (most of them are covered in this book), harder problems may require a *combination* of two (or more) algorithms for their solution. For such problems, try to decompose parts of the problems so that you can solve the different parts independently. We illustrate this decomposition technique using a recent top-level programming problems that combines *three* problem solving paradigms that we have just learned: Complete Search, Divide & Conquer, and Greedy!

## ACM ICPC World Final 2009 - Problem A - A Careful Approach

You are given a scenario of airplane landings. There are 2 ≤ n ≤ 8 airplanes in the scenario. Each airplane has a time window during which it can safely land. This time window is specified by two integers a_i, b_i, which give the beginning and end of a closed interval [a_i, b_i] during which the i-th plane can land safely. The numbers a_i and b_i are specified in minutes and satisfy 0 ≤ a_i ≤ b_i ≤ 1440. In this problem, plane landing time is negligible. Then, your task is to:

- 1. Compute an **order** for landing all airplanes that respects these time windows.
  
  HINT: order = permutation = Complete Search?
- 2. Furthermore, the airplane landings should be stretched out **as much as possible** so that the minimum achievable time gap between successive landings is as large as possible. For example, if three airplanes land at 10:00am, 10:05am, and 10:15am, then the smallest gap is five minutes, which occurs between the first two airplanes. Not all gaps have to be the same, but the smallest gap should be as large as possible!
  
  HINT: Is this similar to ‘greedy activity selection’ problem [4]?
- 3. Print the answer split into minutes and seconds, rounded to the closest second.
  
  See Figure 3.7 for illustration: line = the time window of a plane; star = its landing schedule.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_49_0.png)

**Solution:**

Since the number of planes is at most 8, an optimal solution can be found by simply trying all 8! = 40320 possible orders for the planes to land. This is the **Complete Search** portion of the problem which can be easily solved using C++ STL `next_permutation`.

Now, for each specific landing order, we want to know the largest possible landing window. Suppose we use a certain window length L. We can greedily check whether this L is feasible by forcing the first plane to land as soon as possible and the subsequent planes to land in `max(a[that plane], previous landing time + L)`. This is a **Greedy Algorithm**.

A window length L that is too long/short will overshoot/undershoot `b[last plane]`, so we have to decrease/increase L. We can binary search the answer L - **Divide & Conquer**. As we only want the answer rounded to nearest integer, stopping binary search when error ε ≤ 1e-3 is enough. For more details, please study our AC source code shown on the next page.
