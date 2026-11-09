# ## 3.3 Greedy

An algorithm is said to be greedy if it makes locally optimal choice at each step with the hope of finding the optimal solution. For some cases, greedy works - the solution code becomes short and runs efficiently. But for *many* others, it does not. As discussed in [4], a problem must exhibit two things in order for a greedy algorithm to work for it:

+   1. It has optimal sub-structures.
+   
+      Optimal solution to the problem contains optimal solutions to the sub-problems.
+   
+   2. It has a greedy property (remark: hard to prove its correctness!).
+   
+      If we make a choice that seems best at the moment and solve the remaining subproblems later, we still reach optimal solution. We never have to reconsider our previous choices.

# ### 3.3.1 Classical Example

Suppose we have a large number of coins with different denominations, i.e. 25, 10, 5, and 1 cents. We want to make change with the *least number* of coins used. The following greedy algorithm works for this set of denominations of this problem: Keep using the largest denomination of coin which is not greater than the remaining amount to be made. Example: if the denominations are {25, 10, 5, 1} cents and we want to make a change of 42 cents, we can do: 42-25 = 17 → 17-10 = 7 → 7-5 = 2 → 2-1 = 1 → 1-1 = 0, of total 5 coins. This is optimal.

The coin changing example above has the two ingredients for a successful greedy algorithm:

+   1. It has optimal sub-structures.
+   
+      We have seen that in the original problem to make 42 cents, we have to use 25+10+5+1+1. This is an optimal 5 coins solution to the original problem!
+   
+      Now, the optimal solutions to its sub-problems are contained in this 5 coins solution, i.e.
+      a. To make 17 cents, we have to use 10+5+1+1 (4 coins),
+      b. To make 7 cents, we have to use 5+1+1 (3 coins), etc

+   2. It has a greedy property.
+   
+      Given every amount *V*, we greedily subtract it with the largest denomination of coin which is not greater than this amount *V*. It can be proven (not shown here for brevity) that using other strategy than this will not lead to optimal solution.

However, this greedy algorithm does *not* work for *all* sets of coin denominations, e.g. {1, 3, 4} cents. To make 6 cents with that set, a greedy algorithm would choose 3 coins {4, 1, 1} instead of the optimal solution using 2 coins {3, 3}. This problem is revisited later in Section 3.4.2.

There are many other classical examples of greedy algorithms in algorithm textbooks, for example: Kruskal’s for Minimum Spanning Tree (MST) problem – Section 4.4, Dijkstra’s for Single-Source Shortest Paths (SSSP) problem – Section 4.5, Greedy Activity Selection Problem [4], Huffman Codes [4], etc.

# ### 3.3.2 Non Classical Example

Today’s contest problems usually do not ask for solution of trivial and classical greedy problems. Instead, we are presented with novel ones that requires creativity, like the one shown below.