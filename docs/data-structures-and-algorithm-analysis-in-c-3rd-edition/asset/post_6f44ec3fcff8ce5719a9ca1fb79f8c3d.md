
# Sec. 16.1 Dynamic Programming

subproblems are solved repeatedly, and (2) we can find a suitable way of doing the necessary bookkeeping. Dynamic programming algorithms are usually not implemented by simply using a table to store subproblems for recursive calls (i.e., going backwards as is done by Fibonacci). Instead, such algorithms are typically implemented by building the table of subproblems from the bottom up. Thus, Fibonacci better represents the most common form of dynamic programming than does Fibonacci, even though it doesn’t use the complete table.

## 16.1.1 The Knapsack Problem

We will next consider a problem that appears with many variations in a variety of commercial settings. Many businesses need to package items with the greatest efficiency. One way to describe this basic idea is in terms of packing items into a knapsack, and so we will refer to this as the Knapsack Problem. We will first define a particular formulation of the knapsack problem, then we will discuss an algorithm to solve it based on dynamic programming. We will see other versions of the knapsack problem in the exercises and in Chapter 17.

Assume that we have a knapsack with a certain amount of space that we will define using integer value K. We also have n items each with a certain size such that that item i has integer size k_i. The problem is to find a subset of the n items whose sizes exactly sum to K, if one exists. For example, if our knapsack capacity K = 5 and the two items are of size k_1 = 2 and k_2 = 4, then no such subset exists. But if we add a third item of size k_3 = 1, then we can fill the knapsack exactly with the first and third items. We can define the problem more formally as: Find S ⊂ {1, 2, ..., n} such that ∑_{i∈S} k_i = K.

Example 16.1 Assume that we are given a knapsack size K = 163 and 10 items of sizes 4, 9, 15, 19, 27, 44, 54, 68, 73, 101. Can we find a subset of the items that exactly fills the knapsack? You should take a few minutes and try to do this before reading on and looking at the answer. One solution to the problem is 19, 27, 44, 73.

Example 16.2 Having solved the previous example for knapsack size 163, how hard is it now to solve for a knapsack of size 164? Unfortunately, knowing the answer for 163 is of almost no use at all when solving for 164. One solution is: 9, 54, 101.

If you tried solving these examples, you probably found yourself doing a lot of trial-and-error and a lot of backtracking. To come up with an algorithm, we want an organized way to go through the possible subsets. Is there a way to make the problem smaller, so that we can apply divide and conquer? We essentially have two parts to the input: The knapsack size K and the n items. It probably will not do us much good to try and break the knapsack into pieces and solve the sub-pieces (since we already saw that knowing the answer for a knapsack of size 163 did nothing to help us solve the problem for a knapsack of size 164).

So, what can we say about solving the problem with or without the nth item? This seems to lead to a way to break down the problem. If the nth item is not needed for a solution (that is, if we can solve the problem with the first n − 1 items) then we can also solve the problem when the nth item is available (we just ignore it). On the other hand, if we do include the nth item as a member of the solution subset, then we now would need to solve the problem with the first n − 1 items and a knapsack of size K − k_n (since the nth item is taking up k_n space in the knapsack).

To organize this process, we can define the problem in terms of two parameters: the knapsack size K and the number of items n. Denote a given instance of the problem as P(n, K). Now we can say that P(n, K) has a solution if and only if there exists a solution for either P(n − 1, K) or P(n − 1, K − k_n). That is, we can solve P(n, K) only if we can solve one of the sub problems where we use or do not use the nth item. Of course, the ordering of the items is arbitrary. We just need to give them some order to keep things straight.

Continuing this idea, to solve any subproblem of size n − 1, we need only to solve two subproblems of size n − 2. And so on, until we are down to only one item that either fills the knapsack or not. This naturally leads to a cost expressed by the recurrence relation T(n) = 2T(n − 1) + c = Θ(2^n). That can be pretty expensive!

But... we should quickly realize that there are only n(K + 1) subproblems to solve! Clearly, there is the possibility that many subproblems are being solved repeatedly. This is a natural opportunity to apply dynamic programming. We simply build an array of size n × K + 1 to contain the solutions for all subproblems P(i, k), 1 ≤ i ≤ n, 0 ≤ k ≤ K.

There are two approaches to actually solving the problem. One is to start with our problem of size P(n, K) and make recursive calls to solve the subproblems, each time checking the array to see if a subproblem has been solved, and filling in the corresponding cell in the array whenever we get a new subproblem solution. The other is to start filling the array for row 1 (which indicates a successful solution only for a knapsack of size k_1). We then fill in the succeeding rows from i = 2 to n, left to right, as follows.

if P(n − 1, K) has a solution,

then P(n, K) has a solution else if P(n − 1, K − kₙ) has a solution then P(n, K) has a solution else P(n, K) has no solution.

In other words, a new slot in the array gets its solution by looking at two slots in the preceding row. Since filling each slot in the array takes constant time, the total cost of the algorithm is Θ(nK).

### Example 16.3 Solve the Knapsack Problem for K = 10 and five items with sizes 9, 2, 7, 4, 1. We do this by building the following array.

|  | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| k₁=9 | O | − | − | − | − | − | − | − | − | I | − |
| k₂=2 | O | − | I | − | − | − | − | − | − | O | − |
| k₃=7 | O | − | O | − | − | − | − | I | − | I/O | − |
| k₄=4 | O | − | O | − | I | − | I | O | − | O | − |
| k₅=1 | O | I | O | I | O | I | O | I/O | I | O | I |

Key:

- - -: No solution for P(i, k).
- - O: Solution(s) for P(i, k) with i omitted.
- - I: Solution(s) for P(i, k) with i included.
- - I/O: Solutions for P(i, k) with i included AND omitted.

For example, P(3, 9) stores value I/O. It contains O because P(2, 9) has a solution. It contains I because P(2, 2) = P(2, 9 − 7) has a solution. Since P(5, 10) is marked with an I, it has a solution. We can determine what that solution actually is by recognizing that it includes the 5th item (of size 1), which then leads us to look at the solution for P(4, 9). This in turn has a solution that omits the 4th item, leading us to P(3, 9). At this point, we can either use the third item or not. We can find a solution by taking one branch. We can find all solutions by following all branches when there is a choice.

## 16.1.2 All-Pairs Shortest Paths

We next consider the problem of finding the shortest distance between all pairs of vertices in the graph, called the all-pairs shortest-paths problem. To be precise, for every u, v ∈ V, calculate d(u, v).

One solution is to run Dijkstra’s algorithm for finding the single-source shortest path (see Section 11.4.1) |V| times, each time computing the shortest path from a different start vertex. If G is sparse (that is, |E| = Θ(|V|)) then this is a good

solution, because the total cost will be Θ(|V|² + |V||E| log |V|) = Θ(|V|² log |V|) for the version of Dijkstra’s algorithm based on priority queues. For a dense graph, the priority queue version of Dijkstra’s algorithm yields a cost of Θ(|V|³ log |V|), but the version using MinVertex yields a cost of Θ(|V|³).

Another solution that limits processing time to Θ(|V|³) regardless of the number of edges is known as Floyd’s algorithm. It is an example of dynamic programming. The chief problem with solving this problem is organizing the search process so that we do not repeatedly solve the same subproblems. We will do this organization through the use of the k-path. Define a k-path from vertex v to vertex u to be any path whose intermediate vertices (aside from v and u) all have indices less than k. A 0-path is defined to be a direct edge from v to u. Figure 16.1 illustrates the concept of k-paths.

Define D_k(v, u) to be the length of the shortest k-path from vertex v to vertex u. Assume that we already know the shortest k-path from v to u. The shortest (k + 1)-path either goes through vertex k or it does not. If it does go through k, then the best path is the best k-path from v to k followed by the best k-path from k to u. Otherwise, we should keep the best k-path seen before. Floyd’s algorithm simply checks all the possibilities in a triple loop. Here is the implementation for Floyd’s algorithm. At the end of the algorithm, array D stores the all-pairs shortest distances.

![](img/7ea3c39173f146f675b63b146d1535f3_540_0.png)
