# Chapter 6

# Algorithms 19

(b) Using the notions of compatibility and type, give an O(n)-time dynamic programming algorithm for computing an optimal placement.

6.6. Let us define a multiplication operation on three symbols, $a, b, c$ according to the following table; thus $ab = b, ba = c$, and so on. Notice that the multiplication operation defined by the table is neither associative nor commutative.

| a | b | c |
| a | b | a |
| b | c | a |
| c | a | c |

An efficient algorithm that examines a string of these symbols, *bbb*, and decides whether or not it is possible parenthesize the string in a way that the value of the resulting expression is $a$. For example, on input *bbbab* your algorithm should return yes if $((b(bb))ba)c = a$.

6.7. A subsequence is *palindromic* if it is the same whether read from left to right or right to left. For instance, the sequence

A, C, G, T, G, T, C, A, A, A, A, T, C

has many palindromic subsequences, including $A, C, G, C$ and $A, A, A$ (on the other hand, the subsequence $A, T$ is not palindromic). Devise an algorithm that takes a sequence $x[1..n]$ and returns the length (len) of the longest palindromic subsequence. Its running time should $O(n^2)$.

6.8. Given two strings $x = x_1 \cdots x_n$ and $y = y_1 \cdots y_m$, we wish to find the length of their longest common substring, that is, the largest $k$ for which there do in exist indices $i$ and $j$ with $x_i \cdots x_{i+k-1} = y_j \cdots y_{j+k-1}$. Show how to do this in $O(nm)$.

6.9. A certain string-processing algorithm offers a linear time which splits a string into two pieces. Since this operation involves copying $n$ units of time for a string of length $n$, regardless of the location of the cut. Suppose, you want to break a string into many pieces. The order in which the breaks are made can affect the total running time. For example, if you want to cut a 20-character string at positions 3 and 10, making the first cut at position 3 costs a total of $20 + 17 = 37$, while making position 10 has a better cost of $20 + 10 = 30$.

Give a dynamic programming algorithm, given the $m$ cuts in a string of length $n$, finds the minimum cost of breaking the string into $m$ pieces.

6.10. *Counting heads.* Given integers $n$ and $k$, along with $p_1, \dots, p_n \in [0, 1]$, you want to determine the probability of obtaining exactly $k$ heads when n biased coins are tossed independently at random, where $p_i$ is the probability of the $ith$ coin