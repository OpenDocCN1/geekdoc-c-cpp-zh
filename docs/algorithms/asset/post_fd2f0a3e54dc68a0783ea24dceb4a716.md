
## Chapter 6
## Algorithms 19

(b) Using the notions of compatibility and type, give an O(n)-time dynamic programming algorithm for computing an optimal placement.

6.6. Let us define a multiplication operation on three symbols, $a, b, c$ according to the following table; thus $ab = b, ba = c$, and so on. Notice that the multiplication operation defined by the table is neither associative nor commutative.

| a | b | c |
|---|---|---|
| a | b | a |
| b | c | a |
| c | a | c |

An efficient algorithm that examines a string of these symbols, *bbb*, and decides whether or not it is possible to parenthesize the string in a way that the value of the resulting expression is $a$. For example, on input *bbbab* your algorithm should return yes if $((b(bb))ba)c = a$.

6.7. A subsequence is *palindromic* if it is the same whether read from left to right or right to left. For instance, the sequence

A, C, G, T, G, T, C, A, A, A, A, T, C

has many palindromic subsequences, including $A, C, G, C$ and $A, A, A$ (on the other hand, the subsequence $A, T$ is not palindromic). Devise an algorithm that takes a sequence $x[1..n]$ and returns the length (len) of the longest palindromic subsequence. Its running time should be $O(n^2)$.

6.8. Given two strings $x = x_1 \cdots x_n$ and $y = y_1 \cdots y_m$, we wish to find the length of their longest common substring, that is, the largest $k$ for which there do exist indices $i$ and $j$ with $x_i \cdots x_{i+k-1} = y_j \cdots y_{j+k-1}$. Show how to do this in $O(nm)$.

6.9. A certain string-processing algorithm offers a linear time which splits a string into two pieces. Since this operation involves copying $n$ units of time for a string of length $n$, regardless of the location of the cut. Suppose, you want to break a string into many pieces. The order in which the breaks are made can affect the total running time. For example, if you want to cut a 20-character string at positions 3 and 10, making the first cut at position 3 costs a total of $20 + 17 = 37$, while making position 10 has a better cost of $20 + 10 = 30$.

Give a dynamic programming algorithm, given the $m$ cuts in a string of length $n$, finds the minimum cost of breaking the string into $m$ pieces.

6.10. *Counting heads.* Given integers $n$ and $k$, along with $p_1, \dots, p_n \in [0, 1]$, you want to determine the probability of obtaining exactly $k$ heads when n biased coins are tossed independently at random, where $p_i$ is the probability of the $i$-th coin comes heads. Give an O(nk) algorithm for this task. Assume you can multiply and add two numbers in $[0, 1]$ in $O(1)$ time.

6.11. Given two strings $x = x_1x_2\dots x_n$ and $y = y_1y_2\dots y_m$, we wish to find the length of their longest common subsequence, that is, the largest $k$ for which there are indices $i_1 < i_2 < \dots < i_k$ and $j_1 < j_2 < \dots < j_k$ with $x_{i_1} \dots x_{i_k} = y_{j_1} \dots y_{j_k}$. Show how to do this in $O(nm)$.

6.12. Given a convex polygon $P$ on $n$ vertices in the plane (specified by its $x$ and $y$ coordinates). A *triangulation* of $P$ is a collection of $n-3$ diagonals of $P$ such that no two diagonals intersect (except at their endpoints). Note that a triangulation splits $P$'s interior into $n-2$ disjoint triangles. The cost of a triangulation is the sum of the lengths of the diagonals in it. Is there an efficient algorithm for finding a triangulation of minimum cost? (*Hint*: Label the vertices of $P$ by $1, \dots, n$, starting from an arbitrary vertex and walking clockwise. For $1 \le i < j \le n$, let $A(i, j)$ denote the minimum cost of the triangulation spanned by vertices $i, i+1, \dots, j$).

6.13. Consider the following game. A "dealer" produces a sequence $s_1\dots s_n$ of "cards," face up, where each card $s_i$ has a value $v_i$. Then two players take picking a card from the sequence, but can only pick the first or the last card of the (remaining) sequence. The goal is to collect cards of largest total value. (For example, you can think of the cards as bills of different denominations.) Assume $n$ is even.

- (a) Show a sequence of cards such that it is not optimal for the first player to start by picking the available card of larger value. That is, the natural *greedy* strategy is suboptimal.

- (b) Give an O$(n^2)$ algorithm to compute an optimal strategy for the first player. Given the initial sequence, your algorithm should precompute in $O(n^2)$ time, and then the first player should be able to make each move optimally in $O(1)$ by looking up the precomputed information.

6.14. Cutting cloth. Suppose you have a rectangular cloth of dimensions $X \times Y$, where $X$ and $Y$ are positive integers, and a list of $n$ products that can be made using the cloth. For each product $i \in [1, n]$ you know that a rectangular of cloth of dimensions $a_i \times b_i$ is needed and the final selling price of the product is $c_i$. Assume $a_i, b_i$, and $c_i$ are all integers. You have a machine that can cut any rectangular cloth into two pieces either horizontally or vertically. Design an algorithm that determines the best return on the $X \times Y$ piece of cloth, that is, a strategy for cutting the cloth so that the products made from the resulting pieces give the maximum sum of selling prices. You are free to make as many copies as.

6.15. Suppose two teams, $A$ and $B$, are playing a match to see who wins $n$ games. For each game, $A$ has a probability $p_i$ of winning the $i$-th game. You want to find the probability that $A$ wins exactly $k$ games. Give an efficient algorithm for this.

6.16. The garage sales problem. On a given Sunday, there are garage sales going on $g_1, g_2, \dots, g_n$. For each garage sale $g_i$, you have an estimate of its value $v_i$. You are also given the costs $d_{ij}$ between garage sales. You want to find a tour of garage sales, starting and ending at home, that maximizes total benefit minus transportation costs. Give an algorithm that solves this in time $O(n^2)$.

6.17. Given an unlimited supply of coins of denominations $x_1, x_2, \dots, x_n$, we wish to make change for a value $v$; that is, we wish to find a set of coins whose total value is $v$. This might not be possible: for instance, if the denominations are 5 and 10 then we can make change for 15 but not for 12. Give an O(nv) dynamic programming algorithm for the problem.

6.18. Consider the variation on the change-making problem (Exercise 6.17): you are given denominations $x_1, x_2, \dots, x_n$ and you want to make change for a value $v$, but you are allowed to use each denomination at most once. For instance, if the denominations are 1, 5, 10, 20, then you can make change for 16 = 1 + 15 and for 31 = 1 + 10 + 20 but not for 40 (because you can't use 20 twice). Show how to solve this in O(nv).

6.19. Here is another variation on the change-making problem (Exercise 6.17). Given an unlimited supply of coins of denominations $x_1, x_2, \dots, x_n$, we wish to make change for a value $v$ using at most $k$ coins; we wish to find a set of $\le k$ coins whose total value is $v$. This might not be possible: for instance, if the denominations are 5 and 10 and $k = 6$, then we can make change for 55 but not for 65. Give an efficient dynamic-programming algorithm for the following problem.
