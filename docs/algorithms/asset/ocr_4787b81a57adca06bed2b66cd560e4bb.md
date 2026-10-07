# 180

# Exercises

comes heads. Give an O(nk) algorithm for this task. Assume you can multiply and add two numbers in [0, 1] in O(1) time.

6.11. Given two strings $x = x_1x_2\dots x_n$ and $y = y_1y_2\dots y_m$, we wish to find the length of their longest common subsequence, that is the largest $k$ for which there are indices $i_1 < i_2 <\dots < i_k$ and $j_1 < j_2 <\dots < j_k$ with $x_{i_1} \dots x_{i_k} = y_{j_1} \dots y_{j_k}$. Show how to do this in $O(nm)$.

6.12. Given a convex polygon $P$ on $n$ vertices in the plane (specified by its $x$ and $y$ coordinates). A *triangulation* of $P$ is a collection of $n-3$ diagonals of $P$ such that no two diagonals intersect (except at their endpoints). Note that a triangulation splits $P$'s interior into $n-2$ disjoint triangles. The cost of a triangulation is the sum of the lengths of the diagonals in it. Is there an efficient algorithm for finding a triangulation of minimum cost? (*Hint*: Label the vertices of $P$ by $1, \dots, n$, starting from an arbitrary vertex and walking clockwise. For $1 \le i < j \le n$, let $A(i, j)$ denote the minimum cost of the triangulation spanned by vertices $i, i+1, \dots, j$).

6.13. Consider the following game. A "dealer" produces a sequence $s_1\dots s_n$ of "cards," face up, where each card $s_i$ has a value $v_i$. Then two players take picking a card from the sequence, but can only pick the first or the last card of the (remaining) sequence. The goal is to collect cards of largest total value. (For example, you can think of the cards as bills of different denominations.) Assume $n$ is even.

+   (a) Show a sequence of cards such that it is not optimal for the first player to start by picking the available card of larger value. That is, the natural *greedy* strategy is suboptimal.

+   (b) Give an O$(n^2$) algorithm to compute an optimal strategy for the first player. Given the initial sequence, your algorithm should precompute in $O(n^2)$ time, and then the first player should be able to make each move optimally in $O(1)$ by looking up the precomputed information.

6.14. Cutting cloth. Suppose you have a rectangular cloth of dimensions $X \times Y$, where $X$ and $Y$ are positive integers, and a list of $n$ products that can be made using the cloth. For each product $i \in [1, n]$ you know that a rectangular of cloth of dimensions $a_i \times b_i$ is needed and the final selling price of the product is $c_i$. Assume $a_i, b_i, and c_i$ are all integers. You have a machine that can cut any rectangular cloth into two pieces either horizontally or vertically. Design an algorithm that determines the best return on the $X \times Y$ piece of cloth, that is, a strategy for cutting the cloth so that the products made from the resulting pieces give the maximum sum of selling prices. You are free to make as many copies of a product as you wish, or not if desired.

6.15. Suppose two teams, $A$ and $B$, are playing a match to see who is the first to win $n$ games (for some particular $n$). We can suppose that $A$ and $B$ are equal

> In fact, there is also an $O(n\log^2 n)$ algorithm within your reach.